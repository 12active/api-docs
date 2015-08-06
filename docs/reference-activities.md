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
                    "self": "/activities"
                },
                "data": [],
                "meta": {
                    "endpoints": {
                        "activity_detail": "/activities/{activity_id}",
                        "registered_activities": "/users/registrations",
                        "following_activities": "/users/followings",
                        "giving_activities": "/users/activities"
                    }
                }
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
+ category
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
                                "category": "Crossrunning",
                                "cancelled": false
                            },
                            "links": {
                                "self": "/activities/42",
                                "registration": "/activities/42/registration"
                            }
                        }
                    ],
                "meta": {
                    "endpoints": {
                        "registered_activities": "/users/registrations"
                    }
                }
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
+ category
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
                                "category": "Crossrunning",
                                "cancelled": false
                            },
                            "links": {
                                "self": "/activities/42",
                                "registration": "/activities/42/registration"
                            }
                        }
                    ],
                "meta": {
                    "endpoints": {
                        "following_activities": "/users/followings"
                    }
                }
            }

## Giving activities collection [/users/activities{?variant}]

Activities you - as the trainer - give to others.

If `variant` is set to `full`, data contains all elements from the [detail call](/reference/activities/activity-item).

This might include activities given by your club instead of only activities given by you personally.

This only shows activities up to two weeks in the future.

+ title (string)
+ date (in ISO 8601 format)
+ location
    + title (string)
    + lat
    + lng
+ category
+ cancelled

If `variant` is set to `full`, it also contains:

+ participants

### List all activities [GET]

+ Request normal

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
                                "category": "Crossrunning",
                                "cancelled": false
                            },
                            "links": {
                                "self": "/activities/42",
                                "participants": "/activities/42/participants"
                            }
                        }
                    ]
            }

+ Request full

    + Parameters
    
        + variant: `full`

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
                                "category": "Crossrunning",
                                "cancelled": false,
                                "description": "We verzamelen bij de ingang van het Clingendaelse bos. Dit is waar de Wassenaarsweg kruist met de laan van Clingendael.",
                                "tags": [
                                    "Buiten",
                                    "Intensief",
                                    "Laagdrempelig"
                                ],
                                "subscription": true
                            },
                            "relationships": {
                                "club": {
                                    "data": { "type": "club", "id": 42 }
                                },
                                "participants": {
                                    "links": { "related": "/activities/42/participants" },
                                    "data": { "type": "user", "id": [ 42, 24 ] }
                                }
                            },
                            "links": {
                                "self": "/activities/42",
                                "registration": "/activities/42/registration"
                            }
                        }
                    ]
            }

## Activity item [/activities/{activity_id}]

An activity object has the following attributes:

+ title (string)
+ date (in ISO 8601 format)
+ location
    + title (string)
    + lat
    + lng
+ category
+ cancelled
+ description (string)
+ tags ... array of tags
    + title (string)
+ subscription
+ trainer
    + type
    + id
+ club
    + type
    + id
+ participants (only for trainers)
    + type
    + ids

If subscription is false, a link is provided to the website to arrange payment.

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
                        "date": "2015-04-19T19:00:00+01:00",
                        "location": {
                            "title": "Amsterdamse bos, Amsterdam",
                            "lat": 52.294156,
                            "lng": 4.823620
                        },
                        "category": "Crossrunning",
                        "cancelled": false,
                        "description": "Trailrunning is harlopen in de natuur. ...",
                        "tags": [
                            "Crossrunning",
                            "Hardlopen",
                            "Bootcamp",
                            "Bootcamp & fitness"
                        ],
                        "subscription": true
                    },
                    "relationships": {
                        "trainer": {
                            "data": { "type": "user", "id": 42 }
                        },
                        "club": {
                            "data": { "type": "club", "id": 42 }
                        },
                        "participants": {
                            "links": { "related": "/activities/43154/participants" },
                            "data": { "type": "user", "id": [ 42, 24 ] }
                        }
                    },
                    "links": {
                        "self": "/activities/43154",
                        "registration": "/activities/43154/registration"
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
                            "name": "OUT!-Sport",
                            "logo": "https://dxltue5g50eu3.cloudfront.net/content/icons/1/logo%20OUT!%20met%20url.png"
                        },
                        "links": {
                            "self": "/clubs/42"
                        }
                    }
                ],
                "meta": {
                    "endpoints": {
                        "participants": "/activities/43154/participants",
                        "registration": "/activities/43154/registration"
                    }
                }
            }

## Activity registration [/activities/{activity_id}/registration]

Registering to an activity shows you'll be joining the activity.
The activity will be added to your registered activities collection.
It tells the trainer you want to join the activity.

If an activity gets cancelled, we'll send notifications to all registered users.
These notifications come via email and as push notification via a user's device
(if they [registered for push notifications](/reference/users/user-device).)

Note that right now we also send this notification to all non-registered members of the club.

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
                    "self": "/activities/42/registration"
                },
                "errors":
                    [
                        {
                            "status": "403 Forbidden",
                            "title": "Koop of verleng eerst een abonnement voor deze club.",
                            "links": {
                                "about": "https://www.out2move.nl/account/user/subscriptions"
                            }
                        }
                    ],
                "meta": {
                    "documentation": "http://docs.out2move.apiary.io/"
                }
            }

### Unregister from an activity [DELETE]

Using DELETE unregisters for the activity, allowing refunding of credit for some subscriptions.
Make the request without a request body.

+ Response 204 (application/json)
