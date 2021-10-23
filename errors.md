---
description: How IntaSend handle API errors
---

# Errors reference

IntaSend uses the standard HTTP error codes to communicate failed requests to the APIs. Each failed response is accompanied with a detailed message on the failure.

Here is an example of failed authentication message details with status code 401.

```
{
    "detail": "Authentication credentials were not provided."
}
```

#### Status codes

| 400 | Bad Request -- Your request is invalid.                                                   |
| --- | ----------------------------------------------------------------------------------------- |
| 401 | Unauthorized -- Your API token is wrong.                                                  |
| 403 | Forbidden -- You do not have access to the resource.                                      |
| 404 | Not Found -- The specified resource could not be found.                                   |
| 429 | Too Many Requests -- You're requesting too many requests! Slow down!                      |
| 500 | Internal Server Error -- We had a problem with our server. Try again later.               |
| 503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later. |
