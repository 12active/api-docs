FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# Group Activities

Resources for showing activities and participant registrations.

### Format of collection endpoints

All activity collection endpoints follow the same format.

They only show activities which start today or in a future day.
Activities which already took place this day, are still listed.
Activities are sorted ascending, with earliest date first.

Right now, all activity collections have a relation to the user in some way.
In the future, there will be endpoints for activities based on location or type.

## Activity endpoints [/activities]

## Get possible endpoints [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities",
                    "activity_detail": "/activities/{activity_id}",
                    "registered_activities": "/users/registrations",
                    "following_activities": "/users/followings",
                    "giving_activities": "/users/activities"
                },
                "data": {}
            }

## Registered activities collection [/users/registrations{?variant}]

Activities you - as a participant - planned to join or have joined.

If `variant` is set to `full`, data contains all elements from the [detail call](/reference/activities/activity-item).

+ title (string)
+ date (in ISO 8601 format)
+ location
    + title (string)
    + lat
    + lng
+ default_tag
+ cancelled

+ Parameters
    + variant (optional, string, `full`)

### List all activities [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities",
                    "activity_detail": "/activities/{activity_id}",
                    "following_activities": "/users/followings",
                },
                "data":
                    [
                        {
                            "type": "activity",
                            "id": 42,
                            "attributes": {
                                "title": "Turbo bootcamp",
                                "date": "2015-04-19T19:00:00+01:00",
                                "location": {
                                    "title": "Amsterdamse bos, Amsterdam",
                                    "lat": 52.294156,
                                    "lng": 4.823620
                                },
                                "default_tag": "Crossrunning",
                                "cancelled": false
                            },
                            "links": {
                                "self": "/activities/42",
                                "registration": "/activities/42/registration"
                            }
                        }
                    ]
            }

## Following activities collection [/users/followings{?variant}]

Activities from clubs you are a member of.

If `variant` is set to `full`, data contains all elements from the [detail call](/reference/activities/activity-item).

This only shows activities up to two weeks in the future.

+ title (string)
+ date (in ISO 8601 format)
+ location
    + title (string)
    + lat
    + lng
+ default_tag
+ cancelled

+ Parameters
    + variant (optional, string, `full`)

### List all activities [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities",
                    "activity_detail": "/activities/{activity_id}",
                    "registered_activities": "/users/registrations",
                },
                "data":
                    [
                        {
                            "type": "activity",
                            "id": 42,
                            "attributes": {
                                "title": "Turbo bootcamp",
                                "date": "2015-04-19T19:00:00+01:00",
                                "location": {
                                    "title": "Amsterdamse bos, Amsterdam",
                                    "lat": 52.294156,
                                    "lng": 4.823620
                                },
                                "default_tag": "Crossrunning",
                                "cancelled": false
                            },
                            "links": {
                                "self": "/activities/42",
                                "registration": "/activities/42/registration"
                            }
                        }
                    ]
            }

## Giving activities collection [/users/activities]

Activities you - as the trainer - give to others.

This might include activities given by your club instead of only activities given by you personally.

This only shows activities up to two weeks in the future.

+ title (string)
+ date (in ISO 8601 format)
+ location
    + title (string)
    + lat
    + lng
+ default_tag
+ cancelled
+ participants

### List all activities [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities",
                    "activity_detail": "/activities/{activity_id}",
                },
                "data":
                    [
                        {
                            "type": "activity",
                            "id": 42,
                            "attributes": {
                                "title": "Turbo bootcamp",
                                "date": "2015-04-19T19:00:00+01:00",
                                "location": {
                                    "title": "Amsterdamse bos, Amsterdam",
                                    "lat": 52.294156,
                                    "lng": 4.823620
                                },
                                "default_tag": "Crossrunning",
                                "cancelled": false
                            },
                            "links": {
                                "self": "/activities/42",
                                "participants": {
                                    "related": "/activities/42/participants",
                                    "linkage": { "type": "user", "id": [42,24,44,22] }
                                }
                            }
                        }
                    ]
            }

## Activity item [/activities/{activity_id}]

An activity object has the following attributes:

+ title (string)
+ description (string)
+ cost (optional, string) ... "credit" or "subscription"
+ date (in ISO 8601 format)
+ location
    + title (string)
    + lat
    + lng
+ default_tag
+ tags ... array of tags
    + title (string)
+ cancelled
+ trainer
    + type
    + id
+ club
    + type
    + id
+ participants (only for trainers)
    + type
    + ids

If cost is null, a link should be provided to the website to arrange payment.

+ Parameters
    + activity_id (required, number, `42`) ... ID of the Activity

### View an activity detail [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities/42",
                    "registration": "/activities/42/registration",
                    "participants": "/activities/42/participants",
                },
                "data": {
                    "type": "activity",
                    "id": 42,
                    "attributes": {
                        "title": "Turbo bootcamp",
                        "description": "Trailrunning is harlopen in de natuur. ...",
                        "cost": "credit",
                        "date": "2015-04-19T19:00:00+01:00",
                        "location": {
                            "title": "Amsterdamse bos, Amsterdam",
                            "lat": 52.294156,
                            "lng": 4.823620
                        },
                        "default_tag": "Crossrunning",
                        "all_tags": [
                            "Crossrunning",
                            "Hardlopen",
                            "Bootcamp",
                            "Bootcamp & fitness"
                        ],
                        "cancelled": false
                    },
                    "links": {
                        "self": "/activities/42",
                        "trainer": {
                            "related": "/trainers/42",
                            "linkage": { "type": "user", "id": 42 }
                        },
                        "club": {
                            "related": "/clubs/42",
                            "linkage": { "type": "club", "id": 42 }
                        },
                        "participants": {
                            "related": "/activities/42/participants",
                            "linkage": { "type": "user", "id": [42,24,44,22] }
                        }
                    }
                },
                "included": [
                    {
                        "type": "user",
                        "id": 42,
                        "attributes": {
                            "name": "Pavlov van Beerkoop",
                            "avatar": "pavlov.jpg",
                        },
                        "links": {
                            "self": "/trainers/42"
                        }
                    },
                    {
                        "type": "club",
                        "id": 42,
                        "attributes": {
                            "name": "Calandfit",
                            "logo": "calandfit.png"
                        },
                        "links": {
                            "self": "/clubs/42"
                        }
                    }
                ]
            }

## Activity registration [/activities/{activity_id}/registration]

Registering to an activity shows you'll be joining the activity.
The activity will be added to your registered activities collection.
It tells the trainer you want to join the activity.

+ Parameters
    + activity_id (required, number, `42`) ... ID of the Activity

### Register to an activity [PUT]

Using PUT registers for the activity, withdrawing credit from a subscription.
Make the request without a request body.

Gives an error when the user doesn't have enough credits.
In such case, the client should point the user to the website to buy more credits.

+ Response 204 (application/json)

+ Response 403 (application/json)

    + Body
        
            {
                "links": {
                    "self": "/activities/42/registration",
                    "activity_detail": "/activities/42"
                },
                "errors":
                    [
                        {
                            "status": "403 Forbidden",
                            "code": "insufficient credits",
                            "title": "Koop of verleng eerst een abonnement voor deze club.",
                            "href": "https://www.out2move.nl/account/user/subscriptions"
                        }
                    ]
            }

### Unregister from an activity [DELETE]

Using DELETE unregisters for the activity, allowing refunding of credit for some subscriptions.
Make the request without a request body.

+ Response 204 (application/json)
