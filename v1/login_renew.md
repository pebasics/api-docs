# Description
API Endpoint returns unique token that is replacement for old one sent with requiest. After this endpoint has responded, old token is invalid after this moment. Returns HTML errors and error ID as explained under [errors](https://github.com/pebasics/api-docs/tree/main/Errors).

# API Request
- Method: POST
    - Required
        - token - 128 character lowercase alphanumeric string

# API Location
https://api.peb.rs/v1/login/renew

# Response
HTML status from server is always 200
Content is application/json type
```
    status
        200 - token found, check new_token for updated token value
        4XX - consult [errors](https://github.com/pebasics/api-docs/tree/main/Errors) for further information
    new_token (if status = 200)
        token value - 128 character lowercase alphanumeric string
    valid_till (if status= 200)
        human readable date/time till token is valid. It's using ISO 8601 format (ie. 2023‐09‐25T01:21:20)
    valid_till_unix (if status = 200)
        if end point needs to display various information or to track when token expires (ie. 1695600885)
```

# Examples
Note: these examples are sent via POST method

## Successfull token renewal
Request
```
{"token":"8aca2602792aec6f11a67206531fb7d7f0dff59413145e6973c45001d0087b42d11bc645413aeff63a42391a39145a591a92200d560195e53b478584fdae231a"}
```

Response
```
{
    "status":"200",
    "token":"b0e869f9707a0ceb019795aa8b2c2b06fbee8dc4207da822828b1a1348e9eeb9b38eb12517c150cbce3cd653c09d3314c7dfbf53a54358b97f1d4c0f6b68103f"
}
```

## Token renewal with improperly formatted token
Request
```
{"token":"822828b1a1348e9eeb9b38eb12517c150"}
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
{"token":"b0e869f9707a0ceb019795aa8b2c2b06fbee8dc4207da822828b1a1348e9eeb9b38eb12517c150cbce3cd653c09d3314c7dfbf53a54358b97f1d4c0f6b68103f"}
```

Response
```
{
    "status": 405,
    "message": "Only POST method is allowed.",
    "error_id": 5
}
```
