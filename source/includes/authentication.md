# Authentication
```shell
curl -X GET \
  https://api.eatsa.com/v1/stores \
  -H 'x-authtoken: YOUR_SECRET_KEY'
```

Authenticate your account by including your secret key in every API Request. Keep your API key secure, by not sharing it in publicly accessible platforms such as GitHub, or client side code, or any other public sharing forum.

To authenticate any API request, include the following header `-H "X-Authtoken:YOUR_SECRET_KEY"`.

All API, requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

<aside class="notice">
To request an authentication token for our API please contact your eatsa account manager.
</aside>



