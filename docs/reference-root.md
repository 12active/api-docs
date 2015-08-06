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
                    "self": "/"
                },
                "data": [],
                "meta": {
                    "endpoints": {
                        "users_url": "/users",
                        "activities_url": "/activities",
                        "trainers_url": "/trainers",
                        "clubs_url": "/clubs",
                        "conversations_url": "/conversations"
                    }
                }
            }
