# Errors


## HTTP status codes

 Code | Title | Description
--------- | ------- | -----------
200 | OK | Everything worked as expected.
201	| Created	| The resource was successfully created.
400 | Bad Request | The request was unacceptable, perhaps due to missing a required parameter.
401 | Unauthorized | No valid API key provided.
402 | Request Failed | The parameters were valid but the request failed.
403 | Invalid Scope | The API key provided does not have permission to execute this request.
404 | Not Found | The requested resource does not exist.
429 | Too Many Requests | The user has sent too many requests in a given amount of time.  We recommend decreasing your requests.
500, 502, 503, 504 | Internal Server Error | Something went wrong on our end.

## Error response

> Generic error response (4xx, 5xx)

```json
{
	"id": "NOT_FOUND",
	"message": "Resource not found"
}
```
> Validation failed (400)

```json
{
    "id": "INVALID_INPUT",
    "message": "Invalid request"
}
```

All error messages will return an `id` and a human readable `message`.

Important: Different error `id` types might be added or removed periodically, please ensure your application accepts new error types.

Error id | Code | Description
--------- | ------- | -----------
ERROR | 400  | Invalid request generic error
FIELD_IS_REQUIRED | 400  | Invalid request
INVALID_INPUT | 400  | Invalid request
DUPLICATED_ORDER | 400  | Duplicate order
STORE_CLOSED | 400  | Request can't be processed at this time
NO_PICKUP_LOCATION_AVAILABLE | 400  | There are no pickup locations available
STORE_CLOSED | 400  | Store closed
UNAUTHORIZED | 401  | Unauthorized
FORBIDDEN | 403  | Forbidden
NOT_FOUND | 404  | Resource not found
INTERNAL_SERVER_ERROR | 500  | Internal server error






