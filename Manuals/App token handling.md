# Token Management in the PEB Ecosystem API
## Introduction

App Tokens are the primary method for identifying and authenticating applications within the PEB Ecosystem. Each user can generate a unique App Token via the [app/create](../v1/app.create.md) endpoint or the User Panel on the website.
<br>
Once generated, App Tokens are not retrievable for security reasons. Ensure the App Token is securely stored immediately after generation. Excessive requests for new App Tokens may trigger rate limits or API restrictions.

## Why Use App Tokens?

The App Token system enables secure, scalable, and flexible integration with the PEB Ecosystem API. It provides:
- Authentication: Uniquely identifies each Application using the API.
- Security: Prevents unauthorized access to API endpoints.
- Efficiency: Eliminates the need for user-level credentials in app requests.

> Important: Frequent generation of App Tokens may result in temporary API restrictions. Always securely store generated tokens and avoid unnecessary regeneration.

## Token Generation

Tokens can be created through the [app/create](../v1/app.create.md) endpoint. By default, App Tokens have an indefinite lifetime, unless otherwise specified in the API request or response.

> NOTE: For security purposes, it is recommended to regenerate App Tokens every 30 days to reduce the risk of token compromise.

## Token Validation

Token validity can be verified via the [app/check](../v1/app.check.md) endpoint. This endpoint provides:

- Token Status: Indicates whether the token is valid, expired, or invalid.
- Expiration Details: Displays the token’s expiration date if applicable.
- App Information: Returns relevant details about the associated app.

## Validation Outcomes

When an app token is submitted in an API request, the system evaluates it against three possible scenarios:

- Valid Token with Sufficient Permissions:
    - The API processes the request and returns appropriate data.

- Valid Token with Insufficient Permissions:
    - The API responds with a 4XX error indicating the missing permissions. For more information, refer to the errors documentation.

- Invalid or Missing Token:
    - The API responds with an error, which may occur due to:
        - The token being incorrectly stored or copied.
        - The token expiring.
        - The token being revoked by its creator.

## Token Renewal

Tokens can be renewed at any time using the [app/renew](../v1/app.renew.md) endpoint. Upon renewal:

- The old token is immediately invalidated.
- A new token is issued, ensuring uninterrupted API access.

> Note: Always update the stored token in your app immediately after renewal to avoid interruptions.

## Conclusion

App tokens are an essential part of the PEB Ecosystem API. They ensure secure and efficient integration for your applications.

To use app tokens:
- Generate a App Token via the User Panel or the [app/create](../v1/app.create.md) endpoint.
- Include the token in your app's API requests.
- Validate or renew App Tokens as needed to maintain seamless access.

For further details or troubleshooting, refer to the respective API documentation folders.
