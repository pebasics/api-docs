# Login API Endpoint Documentation
## Description

The `/login` API Endpoint generates a unique token for a user based on the credentials provided in the request. It returns responses in JSON format with appropriate status codes and error messages. Detailed error descriptions can be found in the [Errors](../Errors/) documentation.

## API Endpoint
URL: https://api.peb.rs/v1/login
<br>
Accepted request methods: POST
<br>
Response type `application/json`

> NOTE: The API validates all input values server-side before processing. Client-side validation is strongly recommended to minimize unnecessary API requests and prevent account lockouts caused by excessive failed attempts.

## Request Parameters

Parameters should be sent as `x-www-form-urlencoded`

| Parameter      | Type   | Description                     |
|----------------|--------|---------------------------------|
| `password`     | string | User's password in plain text   |
| `user`         | string | Either user email or username   |

> NOTE: Endpoint accepts either username or email as user login data. Input will be processed by API endpoint to determine which type is provided and processing will continue based on testing results.

## Response Format

The API returns appropriate HTTP status codes for each request. The content type is `application/json`.
<br>
Response Fields:

| Parameter                 | Condition   | Type   | Description                                                                                                                |
|---------------------------|-------------|--------|----------------------------------------------------------------------------------------------------------------------------|
| `status`                  | Always      | int    | Status of request. See [HTML status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)              |
| `require_password_change` | Conditional | bool   | Determines if the user should reset password. Sent only if specific conditions are met                                     |
| `password_change_token`   | Conditional | string | Password reset token. See [password reset](./login.reset.password.md)                                                      |
| `token`                   | Success     | string | A 128-character alphanumeric string                                                                                        |
| `valid_till_unix`         | Success     | int    | Unix timestamp indicating the expiration time of the token (e.g., 1695600885)                                              |
| `valid_till`              | Success     | string | Human-readable date and time until the token is valid, formatted in ISO 8601 (e.g., 2023-09-25T01:21:20) in UTC+0 timezone |
| `error_id`                | Error       | int    | ID of error occured while processing request. See [errors](../Errors/) for further information                             |

## Examples
> NOTE: token values are truncated to 20 characters in examples. Real token will be string of 128 alphanumeric characters.

### 1. Successful Login with Email and Password
Request method: POST
<br>
Request
```JSON
{
    "user": "someone@example.com",
    "password": "Some3xtraLong4nd5afe9assword"
}
```
Response
```JSON
{
    "status": 200,
    "token": "8aca2602792aec6f11af",
    "valid_till": "2023-09-25T01:21:20",
    "valid_till_unix": 1695600885
}
```

### 2. Successful Login with Username and Password
Request method: POST
<br>
Request
```JSON
{
    "user": "someone.example.com",
    "password": "Some3xtraLong4nd5afe9assword4gain"
}
```
Response
```JSON
{
    "status": 200,
    "token": "b0e869f9707a0ceb0197",
    "valid_till": "2023-09-25T01:21:20",
    "valid_till_unix": 1695600885
}
```

### 3. Login Attempt with Improperly Formatted User Field
Request method: POST
<br>
Request
```JSON
{
    "user": "@someone",
    "password": "7h3se94ssw0rds4re8ad"
}
```
Response
```JSON
{
    "status": 400,
    "message": "One of the fields is improperly formatted.",
    "error_id": 8
}
```

### 4. Login Attempt Without Password
Request method: POST
<br>
Request
```JSON
{
    "user": "someone@example.com"
}
```
Response
```JSON
{
    "status": 400,
    "message": "One of the required fields is missing.",
    "error_id": 6
}
```

### 5. Login Attempt Using GET Method
Request method: GET
<br>
Request
```JSON
{
    "user": "someone@example.com",
    "password": "Some3xtraLong4nd5afe9assword"
}
```
Response
```JSON
{
    "status": 405,
    "message": "Only POST method is allowed.",
    "error_id": 5
}
```
