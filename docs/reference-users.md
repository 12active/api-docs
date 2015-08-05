FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# Group Users

Resources for session management and getting information about the currently logged in user.

## User endpoints [/users]

## Get possible endpoints [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/users",
                    "login": "/users/login",
                    "user_detail": "/users/me",
                    "registered_activities": "/users/registrations",
                    "following_activities": "/users/followings",
                    "giving_activities": "/users/activities"
                },
                "data": {}
            }

## User authentication [/users/login]

For now, authentication goes via Basic Auth.
Every call to the api requires the users username and password.

The credential is a base 64 encoded string containing `username:password`.
I.e. `Authorization: Basic c3BvcnR5Z3VydTc4OmxldG1laW4=`.

### Log a user in [POST]

+ username (string)
+ password (string)

+ Request

    + Headers

            Authorization: (required, `Basic c3BvcnR5Z3VydTc4OmxldG1laW4=`) ... Base 64 encoded credentials

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/users/login",
                    "user_detail": "/users/me",
                },
                "data": {},
                "meta": {
                    "interface_type": "participant"
                }
            }

## User item [/users/me]

+ name
+ credit_left ... for information only, as this is combined of multiple clubs
+ activities_done
+ activities_registered
+ multiple_clubs

### View currently logged in user [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/users/me",
                },
                "data": {
                    "type": "user",
                    "id": 42,
                    "attributes": {
                        "name": "Niels Groen",
                        "credit_left": 12,
                        "activities_done": 32,
                        "activities_registered": 2,
                        "multiple_clubs": true
                    },
                    "links": {
                        "registered_activities": "/users/registrations",
                        "following_activities": "/users/followings",
                        "giving_activities": "/users/activities"
                    }
                },
                "meta": {
                    "interface_type": "participant"
                }
            }
