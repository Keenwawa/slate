#   
# Introduction

## API Reference

Welcome to eatsa's API. You can use this API to access all our API endpoints to integrate with the eatsa platform.

Requests can be made to submit and update orders, get an order ETA status, as well as retrieve information about stores.  All requests should be made over SSL. Request and response bodies, including errors, are encoded in JSON. Ensure all request bodies have content type `application/json` and are valid JSON.

All Dates are in UTC expressed using the ISO 8601 format of %Y-%m-%dT%H:%M:%SZ. Example: 2018-04-03T16:02:46Z.


## API Environments

 Environment | Endpoint
-----------------  | --------------------------------
Production | https://api.eatsa.com
Sandbox    | https://api.sandbox.eatsa.com


