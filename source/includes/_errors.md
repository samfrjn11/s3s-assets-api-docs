# Response Codes

The Assets API uses the following response codes:


Response Code | Meaning | Cause
---------- | ------- | -------
200 | Success | Your HTTP requests was successful and a resultset will be returned.
400 | Bad Request | Your request is invalid.
401 | Unauthorized | Your API key is wrong or not supplied.
403 | Forbidden | The resource you're trying to access is not associated to your account/company.
404 | Not Found | The specified asset or resource was not found.
405 | Method Not Allowed | You tried to access an API endpoint with an invalid request method.
429 | Too Many Requests | You exceeded the maximum request amount per minute
500 | Internal Server Error | We have a problem with our server. Try again later.
503 | Service Unavailable | We're temporarily offline for maintenance. Please try again later.
