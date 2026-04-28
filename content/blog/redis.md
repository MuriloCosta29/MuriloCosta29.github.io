 ---
title: "Adding Redis to the Deploy Tracker — and What Caching Actually Solves"
date: 2026-04-28
tags:
  - Redis
---

## The Problem
- Every time the GET request a data in PostgreSQL, this have a time and the problem is here. If the data change, it's ok, right?! Because is necessary the request to view the different data but, **if the data don't change?**, now we have a problem, and the Redis enter to solve this.

## Why Redis
- A Python variable does not have automatic expiration. It also disappears when the process restarts and is not shared between multiple workers. Redis solves these problems because it is a separate service and can expire cached keys automatically with TTL.  
- The Redis store the data in RAM that's made the response faster, because the memory who comes from the hard drive is slowly compared the memory how comes from the RAM.
- I noticed one thing, when you are a beginner(like me), you think: "Why would I use a message broker/database like Redis, just to make it a little faster?", but when I read the book "Grokking Algorithms", I realize: If you are a **beginner**, don't think only in your project, take a little piece of your project and imagine: "If I have 1000 users or 1.000.000, *this would continue running good or too slowly?*, *This is efficient?*". 
- Caching is not just about making one request faster. It is about avoiding repeated work when the answer is already known.


## How I Implemented It

**1.** To implement the Redis we need the `cache.py` -- to create the caching process.  
```
def get_cache(key):
    value = r.get(key)
    if value is not None:
        new_value = json.loads(value)
        return new_value

    return None


# -------------------------------------------------


def to_dict(obj):
    return {c.name: getattr(obj, c.name) for c in obj.__table__.columns}


# -------------------------------------------------


def set_cache(key, data):
    data = [to_dict(item) for item in data]
    value = json.dumps(data, default=str)
    r.set(key, value, ex=300)


# -------------------------------------------------


def delete_cache(key):
    r.delete(key)


```
**2.** `GET /applications` Before and After Redis  

Without(only database):
```
@router.get("/applications")
def list_applications(db: Session = Depends(get_session)):
    return db.query(Application).all()
```

With(Redis integrated):
```
@router.get("/applications")
def list_applications(db: Session = Depends(get_session)):
    cached = get_cache("applications_all")
    if cached:
        return cached
    applications = db.query(Application).all()  # Cache miss, query database
    set_cache("applications_all", applications)
    return applications
```

**Important**: When data changes, the cache must be invalidated to avoid stale results. For example, after creating or updating an application, you should call delete_cache("applications_all").


## Cache Invalidation —  When data change with (POST/PATCH/DELETE)
The cache invalidation is a boring problem! he occurs, because the data in database change, but the data in cache don't. This create inconsistency (stale data).  

- Database -> Original data
- Cache -> Copy database data  


To solve this, I deleted the cached key every time the original data changed.  
So after `POST`, `PATCH`, or `DELETE`, the API calls:  
delete_cache("applications_all")  
The next `GET /applications` will be a cache miss, query PostgreSQL again, and store the fresh result in Redis.


## The Bug That Surprised Me

When I implemented Redis, I tried to cache the SQLAlchemy objects directly.

For my surprise, the API returned `500 Internal Server Error`.

At first, I asked myself: "What did I do wrong?" But the more important question was: "How do I identify the bug?"

In this case, my IDE did not show anything useful. So I went to the terminal logs.

This was an important lesson for me: sometimes the error is not visible in the editor. The application is running, the code looks fine, but the real explanation is in the logs.

After reading the logs, I found the problem: `json.dumps` could not serialize SQLAlchemy objects.

That is when I understood the mistake. Redis was not storing my Python objects directly. In this implementation, I needed to convert my SQLAlchemy models into dictionaries before saving them in the cache.

So I created a `to_dict()` helper:

```
def to_dict(obj):
    return {c.name: getattr(obj, c.name) for c in obj.__table__.columns}
```


My second problem -> In `created_at`, I use `datetime.datetime` to save the date, but `json.dumps()` only understand thinks like:
```
dict
list
str
int
float
bool
None
```
So, how `json.dumps()`, transform a object/type from the module(datetime), in a string?  
to solve it, I use `value = json.dumps(data, default=str)`  
This basic means: finds an object it does not know how to serialize, convert it to a string.  
Because of this, in Deploy Tracker `created_at` become something like this: `"2026-04-19 23:99:99"`😂 (String format).  

Important: Redis was not asking specifically for JSON. I used JSON as the format to serialize my Python data into a string before saving it in Redis.


## What I Learned 
1. **PostgreSQL** -> Hard Disk -> Slower | **Redis** -> RAM -> Faster
2. Speed may seem optional at first, but when handling massive datasets, even a slight delay makes a significant impact on the final result.
3. Caching looks simple, but it creates a new responsibility: keeping the cache consistent with the database.
4. **The database is the source of truth.** Redis stores a temporary copy. When the original data changes, the cache needs to be updated or deleted to avoid stale data.
5. **Logs are part of debugging.** My IDE did not show the real problem, but the terminal logs showed exactly why the API was returning `500`.
6. Redis stores strings/bytes.
