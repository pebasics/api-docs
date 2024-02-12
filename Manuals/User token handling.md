# Introduction
Token is a way of presenting user across ecosystem. Every user can generate unique token by using login endpoint either via custom app or through website.
Also, next to default user token, User can generate new token with limited usage and functionality for other stuff (for example IoT, data update via console app, chatting bots, etc).

# Why token?
Idea is to have wide variety of apps/devices that could use Ecosystem API for various actions.
This includes: website, desktop/laptop apps (Windows, Linux, iOS), mobile phones (android, ios), various devices that can depend on Ecosystem API and much more.

# Token generation
Token is generated using API endpoint located at [login](https://github.com/pebasics/api-docs/v1/login/check.md) and is valid for next 30 days (unless otherwise defined from API response or in request)

# Token checking
Token can be checked via [login/check](https://github.com/pebasics/api-docs/v1/login/check.md) endpoint where token information is returned.

# Token validity
Most of API endpoints will require User token tobe sent with request. In case of valid token, API endpoint will continue with execution and will return appropriate results.
In case that token is invalid (either it expired or is unknown to API) API will respond with appropriate status.

# Token renewal
API token can be renewed at any time before it expires via [login/renew](https://github.com/pebasics/api-docs/v1/login/renew.md). Old token will be unavailable after API has responded with status 200.
