FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# API Root [/]

Following links begins with the root endpoint `/`.
The response contains all starting endpoints to explore.

## Get possible endpoints [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/",
                    "users": "/users",
                    "activities": "/activities",
                    "trainers": "/trainers",
                    "clubs": "/clubs",
                    "conversations": "/conversations"
                },
                "data": {}
            }
