# Error codes messages
There are a few types of error messages you can expect to receive from the SimpleRecommend API. There include:

## 500: Internal Server Error
Something went wrong on our end. If you continue to receive this status code after trying again later, you should contact us so we can help solve the problem.

## 401: Unauthorized
You did not provide a valid API key within the request. Make sure:

1. That you include the API key in the `Api-Key` header, check for spelling and capitalization in the header name.
2. That the API key is, in fact, valid. Maybe you did not enter all characters? Go to your dashboard, view the API key and ensure it matches what you send in your requests.

If problem persists, contact us.

## 400: Bad Request
You have sent an request we consider invalid. Ensure that the HTTP body you send, in the case of a POST request, is valid JSON. Ensure that the JSON object contains the properties specified in our API documentation. Key values may be case sensitive. Make sure you don't mix up underscores, "`_`" with "`-`" or camelcasing. 

## 404: Not Found
You're possibly sending a request to an endpoint that doesn't exist. Check the URL for mistakes. It's possible you're trying to perform an action on an Actor or Provider which does not exist.