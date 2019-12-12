# Email Account

## List

```bash
curl -s -X GET \
-H "Authorization: ApiKey u1@usercase.com:88f61bb2aa5716fb90000000000" \
http://localhost:8001/api/v1/email_account/?domain=forwarder.com
```

> Response

```json
{
    "meta": {
        "limit": 1,
        "next": "/api/v1/email_account/?limit=1&offset=1&domain=forwarder.com",
        "offset": 0,
        "previous": null,
        "total_count": 49
    },
    "objects": [
        {
            "absolute_url": "/user/1@forwarder.com/",
            "aliases": "alias,alias",
            "change_pwd": null,
            "contact": null,
            "create_opt": null,
            "created_at": "Wed, 18 Apr 2018 09:57:29 +0000",
            "domain": "/api/v1/domain/73/",
            "domain_name": "forwarder.com",
            "forwarding_emails": {
                "emails": [
                    "forward_to@example.com",
                    "forward_to22@example.com"
                ],
                "resource_uri": "/api/v1/forwarding_emails/8/"
            },
            "id": 80794,
            "localpart": "1",
            "notification_tasks": [],
            "policy": "/api/v1/policy_user/80876/",
            "priority": 8,
            "resource_uri": "/api/v1/email_account/80794/",
            "state": 0,
            "updated_at": "Wed, 18 Apr 2018 09:57:29 +0000",
            "use_domain_notifications": true,
            "uuid": "e7ce06f1-42ee-11e8-af43-d0509936b9ab"
        },
        {...}
    ]
}
```

List all available email account or filter accounts for certain domain.

`GET https://admin.mailroute.net/api/v1/email_account`

If called without params you'll list all available email accounts from different domains (if you have more then one domain)

Parameter | Type | Description
--- | --- | ---
domain | Int, Str | Fiter accounts by domain id or domain name 

## Get

```bash
# get by email
curl -s -X GET \
-H "Authorization: ApiKey u1@usercase.com:88f61bb2aa5716fb90000000000" \
http://localhost:8001/api/v1/email_account/1@forwarder.com/

# or get by id
curl -s -X GET \
-H "Authorization: ApiKey u1@usercase.com:88f61bb2aa5716fb90000000000" \
http://localhost:8001/api/v1/email_account/80794/
```

> Response

```json
{
    "absolute_url": "/user/1@forwarder.com/",
    "aliases": "alias,alias",
    "change_pwd": null,
    "contact": null,
    "create_opt": null,
    "created_at": "Wed, 18 Apr 2018 09:57:29 +0000",
    "domain": "/api/v1/domain/73/",
    "domain_name": "forwarder.com",
    "forwarding_emails": {
        "emails": [
            "forward_to@example.com",
            "forward_to22@example.com"
        ],
        "resource_uri": "/api/v1/forwarding_emails/8/"
    },
    "id": 80794,
    "localpart": "1",
    "notification_tasks": [],
    "policy": "/api/v1/policy_user/80876/",
    "priority": 8,
    "resource_uri": "/api/v1/email_account/80794/",
    "state": 0,
    "updated_at": "Wed, 18 Apr 2018 09:57:29 +0000",
    "use_domain_notifications": true,
    "uuid": "e7ce06f1-42ee-11e8-af43-d0509936b9ab"
}
```

Get email account resource

`GET /api/v1/email_account/<id>/`

`GET /api/v1/email_account/<email>/`

Parameter | Description
--- | ---
id | Int, email account id
email | String, full email localpart@domain.com

Here is a list of email account object properties.

Property | Description
--- | ---
absolute_url | Url for user page in our control panel
aliases | Comma separated list of localpart aliases of this account
change_pwd | Null, See update password section
create_opt | Null, See update password section
created_at | Creation date in format: "Wed, 18 Apr 2018 09:57:29 +0000"
updated_at | Last update time in format: "Wed, 18 Apr 2018 09:57:29 +0000"
domain | URI that point to domain resource through this API
domain_name | Verbose domain name
forwarding_emails | Object. `emails` - list of forwarding emails for this account, `resource_uri` - uri for forwarding emails resource
id | Unique ID
localpart | The localpart of the email address
notification_tasks | List of URIs for quarantine notifications resources
policy | URI for user content filter policy resource
resource_uri | Account resource direct URI
state | Int, `0` - standard account, `1` - provisional account, `2` - distribution list
use_domain_notifications | Bool, Is using domain's quarantine notifications?
uuid | Unique uuid

## Update

```bash
curl -s --dump-header - -X PUT \
    -H 'Content-Type: application/json' \
    -H 'Authorization: ApiKey u1@usercase.com:88f61bb2aa5716fb90000000000' \
    --data '{
        "absolute_url": "/user/admin@example.com/",
        "aliases": "",
        "change_pwd": null,
        "contact": null,
        "create_opt": null,
        "created_at": "Wed, 14 Nov 2018 10:32:29 +0000",
        "domain": "/api/v1/domain/91/",
        "domain_name": "example.com",
        "forwarding_emails": {
            "emails": [],
            "resource_uri": null
        },
        "id": 203696,
        "localpart": "admin",
        "notification_tasks": [],
        "policy": "/api/v1/policy_user/203796/",
        "priority": 8,
        "resource_uri": "/api/v1/email_account/203696/",
        "state": 0,
        "updated_at": "Fri, 23 Aug 2019 14:22:49 +0000",
        "use_domain_notifications": true,
        "uuid": "95c0bf05-e7f8-11e8-aed3-acde48001122"
      }'\
    http://localhost:8001/api/v1/email_account/203696/
```

> Response

```json
HTTP/1.0 200 OK
Date: Fri, 23 Aug 2019 14:52:38 GMT
Server: WSGIServer/0.1 Python/2.7.10
Vary: Accept, Cookie
Content-Length: 612
Content-Type: application/json

{
    "absolute_url": "/user/admin@example.com/",
    "aliases": "",
    "change_pwd": null,
    "contact": null,
    "create_opt": null,
    "created_at": "Wed, 14 Nov 2018 10:32:29 +0000",
    "domain": "/api/v1/domain/91/",
    "domain_name": "example.com",
    "forwarding_emails": {
        "emails": [],
        "resource_uri": null
    },
    "id": 203696,
    "localpart": "admin",
    "notification_tasks": [],
    "pk": "203696",
    "policy": "/api/v1/policy_user/203796/",
    "priority": 8,
    "resource_uri": "/api/v1/email_account/203696/",
    "state": 0,
    "updated_at": "Fri, 23 Aug 2019 14:54:45 +0000",
    "use_domain_notifications": true,
    "uuid": "95c0bf05-e7f8-11e8-aed3-acde48001122"
}
```

Update email account with new data.

`PUT https://admin.mailroute.net/api/v1/email_account/<id>/`

`PUT https://admin.mailroute.net/api/v1/email_account/<email>/`

Send entire resource in request body to update email account.

<aside class="notice">
A PUT request requires that the entire resource representation be enclosed. Missing fields may cause errors, or be filled in by default values. This means that you have to send entire resource with the same fields (but changed value) as returned by GET. Basically you have to GET resource, change some data and send entire set via PUT to update it. If this is not desired you can make "partial update" through PATCH if this resource accepts it.
</aside>

Properties that can be changed.

Property | Description
--- | ---
localpart |
state |
use_domain_notifications |
send_welcome | `true` will resend welcome email to user

We will return updated resource.

## Partial Update

> Turn off email account notifications (use domain settings)

```shell
curl -s --dump-header - -X PATCH \
  -H 'Content-Type: application/json' \
  -H 'Authorization: ApiKey u1@usercase.com:88f61bb2aa5716fb90000000000' \
  --data '{
      "use_domain_notifications": false
    }'\
  http://localhost:8001/api/v1/email_account/203696/
```

> Response with 202 code and updated resource

```json
HTTP/1.0 202 Accepted
Date: Fri, 23 Aug 2019 15:05:03 GMT
Server: WSGIServer/0.1 Python/2.7.10
Vary: Accept, Cookie
Content-Length: 597
Content-Type: application/json

{
  "absolute_url": "/user/admin@example.com/",
  "aliases": "",
  "change_pwd": null,
  "contact": null,
  "create_opt": null,
  "created_at": "Wed, 14 Nov 2018 10:32:29 +0000",
  "domain": "/api/v1/domain/91/",
  "domain_name": "example.com",
  "forwarding_emails": {
    "emails": [],
    "resource_uri": null
  },
  "id": 203696,
  "localpart": "admin",
  "notification_tasks": [],
  "policy": "/api/v1/policy_user/203796/",
  "priority": 8,
  "resource_uri": "/api/v1/email_account/203696/",
  "state": 0,
  "updated_at": "Fri, 23 Aug 2019 15:05:03 +0000",
  "use_domain_notifications": false,
  "uuid": "95c0bf05-e7f8-11e8-aed3-acde48001122"
}
```

In some cases, you may not want to send the entire resource when updating. To update just a subset of the fields, we can send a PATCH request to the detail endpoint.

`PATCH https://admin.mailroute.net/api/v1/email_account/<id>/`

`PATCH https://admin.mailroute.net/api/v1/email_account/<email>/`

Properties that can be changed.

Property | Description
--- | ---
localpart |
state | Int, `0` - standard account, `1` - provisional account, `2` - distribution list
use_domain_notifications | `true` to use domain notifications, `false` to use user notifications
send_welcome | `true` will resend welcome email to user

Send only fields that have to be updated e.g.

```json--inline
{
  "use_domain_notifications": false
}
```

## Delete

```shell
curl -s --dump-header - -X DELETE \
  -H 'Content-Type: application/json' \
  -H 'Authorization: ApiKey u1@usercase.com:88f61bb2aa5716fb90000000000' \
  http://localhost:8001/api/v1/email_account/203696/
```

> We will respond with 204 status

```json
HTTP/1.0 204 No Content
Date: Fri, 23 Aug 2019 15:14:23 GMT
Server: WSGIServer/0.1 Python/2.7.10
Content-Length: 0
Vary: Accept, Cookie
```

`DELETE https://admin.mailroute.net/api/v1/email_account/<id>/`

`DELETE https://admin.mailroute.net/api/v1/email_account/<email>/`

We will respond with 204 code.


## Update password

```shell
curl -s --dump-header - -X PATCH \
  -H 'Content-Type: application/json' \
  -H 'Authorization: ApiKey u1@usercase.com:88f61bb2aa5716fb90000000000' \
  --data '{
    "confirm_password": "qazxswedc",
    "password": "qazxswedc",
    "change_pwd": true
  }' \
  'http://localhost:8001/api/v1/email_account/user1@example.com/'
```

```json
HTTP/1.0 202 Accepted
Date: Fri, 23 Aug 2019 15:21:43 GMT
Server: WSGIServer/0.1 Python/2.7.10
Vary: Accept, Cookie
Content-Length: 654
Content-Type: application/json

{
  "absolute_url": "/user/user1@example.com/",
  "aliases": "",
  "change_pwd": null,
  "confirm_password": "qazxswedc",
  "contact": null,
  "create_opt": null,
  "created_at": "Fri, 23 Aug 2019 14:19:57 +0000",
  "domain": "/api/v1/domain/91/",
  "domain_name": "example.com",
  "forwarding_emails": {
    "emails": [],
    "resource_uri": null
  },
  "id": 216915,
  "localpart": "user1",
  "notification_tasks": [],
  "password": "qazxswedc",
  "policy": "/api/v1/policy_user/217045/",
  "priority": 8,
  "resource_uri": "/api/v1/email_account/216915/",
  "state": 0,
  "updated_at": "Fri, 23 Aug 2019 15:21:43 +0000",
  "use_domain_notifications": true,
  "uuid": "15376d5c-c5b1-11e9-bee0-acde48001122"
}
```

`PATCH https://admin.mailroute.net/api/v1/email_account/<id>/`

`PATCH https://admin.mailroute.net/api/v1/email_account/<email>/`

To update password send following data to email account resource url:

```text
{
   "confirm_password": "new password here",
   "password": "new password here",
   "change_pwd": true
}
```


## Reset password

```shell
curl -s --dump-header - -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: ApiKey u1@usercase.com:88f61bb2aa5716fb90000000000' \
  --data '{
    "accounts": [
      "/api/v1/email_account/user1@example.com/"
    ],
    "reset_pwd": true
  }' \
  http://localhost:8001/api/v1/email_account/mass_resend_welcome/
```

> Response

```http
HTTP/1.0 202 Accepted
Date: Fri, 23 Aug 2019 15:33:20 GMT
Server: WSGIServer/0.1 Python/2.7.10
Vary: Accept, Cookie
Content-Length: 0
Content-Type: text/html; charset=utf-8
```

Drop user password and send new autogenerated password.

Parameters:

Parameter | Description
--- | ---
accounts | list of email account resource uri's which you want to reset password
reset_pwd | set `true` to reset password and sent it in email, or `false` to just send welcome email to user with link to our control panel without password reset.

## Delete

```shell

```

> Response

```json

```


