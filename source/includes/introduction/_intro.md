# API Introduction

> API base url:

```console
https://admin.mailroute.net/
```

The API is a REST-style API providing access to all aspects of the MailRoute Service configuration. Everything you see in our own interface at https://admin.mailroute.net is done through this API and all of that functionality is available to you.

Our API accepts [JSON-encoded](https://json.org) request bodies and returns JSON-encoded responses.

Our examples below will all use `curl` to show the details of the API calls and their returned values, but you can call our API from whatever language you prefer - anything that can issue HTTP requests can talk to our system.

## Data Format

We support only `json` format. All requests must send payloads in json format too.
Add this headers to your requests.

```text
Accept: application/json
Content-Type: application/json
```

## Authentication

```shell
curl -s \
-H "Content-Type: application/json" \
-H "Authorization: ApiKey user@example.com:123456789abcde" \
https://admin.mailroute.net/api/v1/
```

> Example response:

```json
{
    "customer": {
        "list_endpoint": "/api/v1/customer/",
        "schema": "/api/v1/customer/schema/"
    },
    "domain": {
        "list_endpoint": "/api/v1/domain/",
        "schema": "/api/v1/domain/schema/"
    },
    "email_account": {
        "list_endpoint": "/api/v1/email_account/",
        "schema": "/api/v1/email_account/schema/"
    },
   ...
}
```

You authenticate to the MailRoute API by providing one of your API keys in the HTTP request. You can find your API key on your account's settings page. Your API key has all the privileges of your login account, so be sure to keep it secret!

Authentication to the API occurs via HTTP `Authorization` header. Provide a header in the format: 

`Authorization: ApiKey <login>:<apikey>`

All API calls must be made over HTTPS. Calls over plain HTTP will fail. You must authenticate every request.

## Errors

```shell
curl -k --dump-header - -X PUT \
-H 'Content-Type: application/json' \
-H "Authorization: ApiKey <login>:<key>" \
--data '{}' \
https://admin.mailroute.net/api/v1/preferred_languages/98/
```

> Response with 400 error code and details.

```shell
HTTP/1.0 400 Bad Request
Date: Wed, 21 Aug 2019 15:05:05 GMT
Server: WSGIServer/0.1 Python/2.7.10
Vary: Cookie
Content-Length: 59
Content-Type: application/json

{"error_message": "domain or email_account field required"}
```

HTTP Response codes are used to indicate the success or failure of an API request.

Codes in the 2xx range indicate success, those in the 4xx range indicate that there's an error in the provided information (ie, missing parameter, duplicate entry, etc). Errors in the 5xx range indicate an error in the MailRoute servers.

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- You have no permission to interact with resource.
404 | Not Found.
405 | Method Not Allowed.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

Also we will send error details in response text (it's json too)

## Paginated Results

> Get 40 accounts per page

```bash
curl -k --dump-header - -X PUT \
-H 'Content-Type: application/json' \
-H "Authorization: ApiKey <login>:<key>" \
--data '{}' \
https://admin.mailroute.net/api/v1/email_account/?limit=40
```

> Response

```json
{
    "meta": {
        "limit": 40,
        "next": "/api/v1/email_account/?limit=40&offset=40",
        "offset": 0,
        "previous": null,
        "total_count": 49
    },
    "objects": [
        ...
    ]
}
```

By default, you get a paginated set of objects (20 per page is the default).
You can overwrite defaults with GET params.

Parameter | Type | Desctiption
--------- | ---- | -----------
limit | Int | Limit objects per page in returned data
offset | Int | Skip this number of objects

We will return meta object in response at any listing endpoint.
In the meta, you get a `previous` & `next`. If available, these are URIs to the previous & next pages. There is also current limit, offset and `total_count` total records.

You get a list of resources/objects under the `objects` key.
Each resources/object has a `resource_uri` field that points to the detail view for that object.


