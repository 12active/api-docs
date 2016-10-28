FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# Fitmanager

Fitmanager offers an API allowing sports trainers an participants
to communicate about sport activities.

The API follows the [json:api syntax](http://jsonapi.org/).

All endpoints share the same base `https://club.fitmanager.com/api`.

### Client identification

Clients need their app registered to be able to use the API.
Upon registering you'll receive a `client_id` and `client_secret`.

You make calls by adding both as url parameters.
I.e. `GET /users/me?client_id=foo&client_secret=bar`.

### User authentication

User authentication is handled via Basic Auth and JWT. Each call to the api should be sent with a JWT token, there are no session ids.
The JWT token, can be obtained via a specific authentication API call [/users/authenticate call](/reference/users/user-authenticate) , which accepts the following kinds of login information via the Authorization:Basic header.

By default, it requires the user's username and password.
The credential is a base 64 encoded string containing `username:password`.
I.e. `Authorization: Basic c3BvcnR5Z3VydTc4OmxldG1laW4=`.

Users should authenticate via Facebook if they signed up at Fitmanager using Facebook.
Clients are responsible for handling oauth with Facebook using Fitmanager provided app info.
After handling oauth, the user should be checked at Fitmanager by sending their oauth access token.
I.e. `Authorization: Out2MoveFacebookLogin: access_token=xyz`.

Note right now users can only use one login method, either username/password *or* Facebook.
This depends on how they signed up at Fitmanager.

When the login information is accepted, the authorization method will return the user details along with a 'token' field. This token fields contains the JWT token that can be used for other request. The JWT token needs to be sent in the Authorization:Bearer header
I.e. `Authorization: Bearer qwdfsdfsdfsferewrsf34refds...`.

### Following links

You'll be able to navigate through the api using links provided in each response.
It is recommend to follow the `links` values to retrieve resources instead of constructing your own URLs.
This keeps the client decoupled from implementation details.

### Standard attributes

Each response can contain the following attributes:

+ `links` ... array of links
    + `self` ... link to the resource just requested
                 this may be a dynamic url for collections and the like
                 i.e. for an `/featured-activity-of-the-day` endpoint
                 as apposed to `data.links.self` which gives the exact same resource

+ `data` ... object, or array of objects
    + `type` ... the type of resource, i.e. `activity`
    + `id`
    + `attributes`
        + primary data
    + `relationships`
        + some related resource
            + `links`
                + `related` ... link to the related resource, i.e.: `/author/{id}`
            + `data` ... info to find back resources in the `included` array
                + `type`
                + `id` ... int or array of ints
    + `links`
        + `self` ... link to the resource just requested, i.e.: `/endpoint/{id}`
        + more links ... linking to related resources
                         often going lower or higher in the endpoint structure

+ `included` ... array of objects
    + `type`
    + `id`
    + `attributes`
        + primary data
    + `links`
        + `self` ... link to this resource's full data

+ `meta` ... object
    + non primary data

You can read more about the structure in the [json:api specification](http://jsonapi.org/).

### Possible status codes

+ ok (200)
+ created (201)
+ no_content (204)
+ bad_request (400)
+ unauthorized (401)
+ forbidden (403)
+ not_found (404)
+ method_not_allowed (405)
+ unprocessable_entity (422)
+ internal_server_error (500)

### Versioning

Versioning is optional. By default, you'll get the most recent version of the api specificiation.

For production environments, it is recommended to request a specific version.
To do so, send an `Accept` header specifying the version.

`application/vnd.api+json.v1`

If you want to provide an `Accept` header without versioning, you can use
`application/vnd.api+json` or just plain `application/json`.

### Internationalization

We accept the `Accept-Language` header to send along i18n'd messages.
This happens mostly for errors and in some specific error-alike situations.
For example, a participant with a payment due, see [participant details](/reference/participants/activity-participant).

In the response, a corresponding `Content-Language` header is included.
In case there is no i18n for the requested language, we'll pass English.

### Push notifications

For mobile apps, we can send push notifications to a user's device.
If users don't allow to receive push notifications, they'll receive them via email.

Right now we send notifications for new conversation messages and cancelled activities.
Detailed info is at the description of those endpoints.
Notifications are generally send to all members and trainers of a club.

To be able to receive push notifications, you need to register the device.
To make sure unauthorized users don't receive them, you need to unregister the device once the user logs out.
See [device registration](/reference/users/user-device) and [notification testing](/reference/users/test-notification) for details.

All push notifications include additional metadata:

+ title
+ type
+ *_id

For example:

        {
            "title": "Nieuw bericht",
            "type": "new-message",
            "conversation_id": 42
        }
