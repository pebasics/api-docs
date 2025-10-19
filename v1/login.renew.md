# Description
API Endpoint returns unique token that is replacement for old one sent with requiest. After this endpoint has responded, old token is invalid after this moment. Returns HTML errors and error ID as explained under [errors](https://github.com/pebasics/api-docs/tree/main/Errors).

# API Request
## API endpoint
URL: https://api.peb.rs/v1/login/renew
<br>
Accepted request methods: POST

| Parameter      | Type   | Description                         |
|----------------|--------|-------------------------------------|
| `token`        | string | 128 character alphanumeric string   |

# API Location
https://api.peb.rs/v1/login/renew

# Response
Content-Type is `application/json`
```
    status
        200 - token found, check new_token for updated token value
        4XX - consult [errors](https://github.com/pebasics/api-docs/tree/main/Errors) for further information
    new_token (if status = 200)
        token value - 128 character alphanumeric string
    valid_till (if status= 200)
        human readable date/time till token is valid. It's using ISO 8601 format (ie. 2023‐09‐25T01:21:20)
    valid_till_unix (if status = 200)
        if end point needs to display various information or to track when token expires (ie. 1695600885)
```

# Examples
> NOTE: Tokens are truncated to maximum length of 20 characters. tokens are 128 alphanumeric string.
## Successfull token renewal
Request method: POST
Request
```
{
    "token":"0dff59413145e6973c45"
}
```
Response
```
{
    "status": 200,
    "token": "8aca2602792aec6f11af",
    "valid_till": "2023-09-25T01:21:20",
    "valid_till_unix": 1695600885
}
```

## Token renewal with improperly formatted token
Request
```
{"token":"822828b1a1348e9eeb9b"}
```

Response
```
{
    "status": 400,
    "message": "One of fields is improperly formatted.",
    "error_id": 8
}
```

## Token renewal attempt with GET method
Request
```
{"token":"cd653c09d3314c7dfbf5"}
```

Response
```
{
    "status": 405,
    "message": "Only POST method is allowed.",
    "error_id": 5
}
```
