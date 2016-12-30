---
layout: post
title: How to Disable HSTS
---

In Chrome, you can clear the HSTS state by going into `about:net-internal`. 
You may also have to clear the cache, since `config.force_ssl = true` also uses a 301 (permanent) redirection.
In addition, you could also make your application send an STS header with `max-age=0`. In your controller:

```
response.headers["Strict-Transport-Security"] = 'max-age=0'
```