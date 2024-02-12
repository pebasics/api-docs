# Description
API Endpoint returns unique token for user whos data is sent in request. Returns HTML errors and error ID as explained under [errors](https://github.com/pebasics/api-docs/tree/main/Errors).

# API Request
- Method: POST
    - One of the following:
        - email - plain text
        - username - plain text
    - Requested
        - password - plain text

*Note: all values are checked by API endpoint prior to processing, but client side verification is advisable to prevent users from being locked out due to API call limitations.

# Response
HTML status from server is always 200
Content is application/json type
    status:
        200 - all OK, sends token value
        4XX - consult APIS-A-5 for further information
    token (if status = 200)
        token value - 128 character lowercase alphanumeric value
    valid_till (if status= 200)
        human readable date/time till token is valid. It's using ISO 8601 format (ie. 2023‐09‐25T01:21:20)
    valid_till_unix (if status = 200)
        if end point needs to display various information or to track when token expires (ie. 1695600885)

# Examples
Note: these examples are sent via POST method
## Successfull login with email and password
Request
```
["email":"someone@example.com","password":"Some3xtraLong4nd5afe9assword"]
```

Response
```
{
    "status":"200",
    "token":"8aca2602792aec6f11a67206531fb7d7f0dff59413145e6973c45001d0087b42d11bc645413aeff63a42391a39145a591a92200d560195e53b478584fdae231a"
}
```

## Successfull login with username and password
Request
```
["username":"someone.example","password":"Some3xtraLong4nd5afe9assword4gain"]
```

Response
```
{
    "status":"200",
    "token":"b0e869f9707a0ceb019795aa8b2c2b06fbee8dc4207da822828b1a1348e9eeb9b38eb12517c150cbce3cd653c09d3314c7dfbf53a54358b97f1d4c0f6b68103f"
}
```

## Login attempt with improperly formatted email
Request
```
["email":"someone@example","password":"7h3se94ssw0rds4re8ad"]
```

Response
```
{
    "status": 400,
    "message": "One of fields is improperly formatted.",
    "error_id": 8
}
```

## Login attempt without password
Request
```
["email":"someone@example.com"]
```

Response
```
{
    "status": 400,
    "message": "One of required fields is missing.",
    "error_id": 6
}
```

## Login attempt with GET method
Request
```
["email":"someone@example.com","password":"Some3xtraLong4nd5afe9assword"]
```

Response
```
{
    "status": 405,
    "message": "Only POST method is allowed.",
    "error_id": 5
}
```
