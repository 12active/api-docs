FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# Out2Move

Out2Move offers an API allowing sports trainers an participants
to communicate about sport activities.

The API follows the [json:api syntax](http://jsonapi.org/).

## Authentication

For now, authentication goes via Basic Auth.
Full authentication is required for every call to the api, there are no session ids.

By default, it requires the user's username and password.
The credential is a base 64 encoded string containing `username:password`.
I.e. `Authorization: Basic c3BvcnR5Z3VydTc4OmxldG1laW4=`.

Users should authenticate via Facebook if they signed up at Out2Move using Facebook.
Clients are responsible for handling oauth with Facebook using Out2Move provided app info.
After handling oauth, the user should be checked at Out2Move by sending their oauth access token.
I.e. `Authorization: Out2MoveFacebookLogin: access_token=xyz`.

Note right now users can only use one login method, either username/password *or* Facebook.
This depends on how they signed up at Out2Move.

As full authentication is needed for every call, there is no specific login endpoint.
Testing for a successful login can be best done using the [/users/me call](/reference/users/user-item).

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
    + more links ... linking to related resources
                     often going lower or higher in the endpoint structure

+ `data` ... object, or array of objects
    + `type` ... the type of resource, i.e. `activity`
    + `id`
    + `attributes`
        + primary data
    + `links`
        + `self` ... link to the resource just requested, i.e.: `/endpoint/{id}`
        + some related resource
            + `related` ... link to the related resource, i.e.: `/author/{id}`
            + `linkage` ... way to find back resources in the `included` array
                + `type`
                + `id` ... int or array of ints

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
