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
                    "user_detail": "/users/me",
                    "registered_activities": "/users/registrations",
                    "following_activities": "/users/followings",
                    "giving_activities": "/users/activities"
                },
                "data": {}
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
