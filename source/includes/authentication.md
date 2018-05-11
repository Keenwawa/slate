# Authentication
```shell
curl -X GET \
  https://api.eatsa.com/v1/stores \
  -H 'x-authtoken: YOUR_SECRET_KEY'
```

To authenticate an API request include the following header `x-authtoken: YOUR_SECRET_KEY` in every request.

<aside class="notice">
To request an authentication token for our API please contact your account manager.
</aside>
