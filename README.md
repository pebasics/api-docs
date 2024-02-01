#PEB Ecosystem API documentation
---
# Why documentation?
Documentation is required as idea behind PEB Ecosystem is to be free and open for its members and content creators to be free to use which ever app they preffer to have integration with API.

# Endpoints
API consists of various endpoints, all being well documented in respective folder. Each endpoint lives inside its API version and category.
Endpoints can have multiple versions, mainly determined by API version itself. As newer versions of endpoints are being developed, older ones will report as outdated (they will still provide data till end date is reached). Once an end date is reached, endpoint will return either 404 HTML code or will redirect request to newer version of that endpoint.

# Errors and error handling
Every API endpoint has a list of errors that could occur either due to user missinput or missing field, or due to server side errors. Errors are listed inside Errors folder.
