---
layout: post
title: "Laravel Query Scopes and Attributes"
date:   2018-09-02 17:00:00 +0800
categories: laravel
author: "John Aldrin Plata"
meta: "laravel"
---

-- DRAFT --

You might be using a repository pattern to encapsulate your database call. But sometimes, you could just use scope queries. Blah Blah

... a method should be prefix with `scope` followed by the method name and should accept a query as the first parameter.
```php
/**
  * Query to return only published posts.
  *
  * @param \Illuminate\Database\Eloquent\Builder $query
  * @return \Illuminate\Database\Eloquent\Builder
  */
public function scopePublished($query) {
    return $query->where('is_published', true);
}
```

To use it, we could just call
```php
Post::published();
```

It will return a query builder so we can chain more methods. For example, we want to get all the published blog posts that has reached at least 1000 views

```php
Post::published()->where('views', '>=', 1000)->get();
```

Or you might want to return a collection immediately after the function call.

```php
public function scopePublished($query) {
    return $query->where('is_published', true)->get();
}
```

Notice we added a call to `get()` and the function now returns a collection of published posts.

```php
$posts = Post::published();
```


```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Review extends Model
{
    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = ['user_id', 'title', 'rate', 'content'];
}
```