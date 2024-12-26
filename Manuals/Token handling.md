# Token Management in the PEB Ecosystem API
## Introduction

Tokens are the primary method for identifying and authenticating users within the PEB Ecosystem. Each user can generate a unique token via the login endpoint, either through the website or a custom application.

In addition to the default user token, users can generate specialized tokens with limited functionality for specific use cases, such as:

- IoT devices
- Data synchronization through various apps
- Chatbots and automation

## Why Use Tokens?

The token system ensures secure, flexible, and efficient integration with the PEB Ecosystem API. It allows a wide range of devices and applications to interact with the API seamlessly, including:

- Websites
- Desktop and laptop applications (Windows, Linux, macOS)
- Mobile apps (Android, iOS)
- IoT devices and other connected systems

# Token Generation

Tokens are generated via the [login](../v1/login.md) endpoint. By default, each token is valid for 30 days unless a different duration is specified in the API response or the request itself.
# Token Validation

The validity of a token can be checked using the [login/check](../v1/login.check.md) endpoint. This endpoint returns detailed information about the token's status, including its expiration date and associated user data.
Validation Scenarios:

- Valid Token: If the token is valid, the API will proceed with the request and return the appropriate data if aplicable.
- Invalid Token: If the token has expired or is unknown, the API will respond with an appropriate HTTP status code and error message.

## Token Renewal

Tokens can be renewed at any time before they expire via the [login/renew](../v1/login.renew.md) endpoint. Once renewed:

- The old token becomes invalid immediately.
- A new token is issued, ensuring uninterrupted access to the API.

## Conclusion

The token system in the PEB Ecosystem API provides a secure and versatile mechanism for user authentication and application integration. By leveraging token-based access, developers can create innovative solutions that seamlessly interact with the ecosystem while ensuring user data remains protected.

For more details or troubleshooting, refer to the respective API documentation folders.
