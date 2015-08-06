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
                    "self": "/users"
                },
                "data": [],
                "meta": {
                    "endpoints": {
                        "user_detail": "/users/me",
                        "registered_activities": "/users/registrations",
                        "following_activities": "/users/followings",
                        "giving_activities": "/users/activities"
                    }
                }
            }

## User item [/users/me]

+ name
+ avatar
+ phone
+ activities_done
+ last_activity_in_days
+ multiple_clubs
+ interface_type (trainer or participant)

For participants, this can be extended with:

+ club
    + credit_left
    + subscription_name
    + subscription_date_start
    + subscription_date_end
    + subscription_payment_due
    + last_activity

For trainers, this can be extended with:

+ club
    + name
    + logo

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
                        "name": "Lode Claassen",
                        "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                        "phone": "",
                        "activities_done": 32,
                        "last_activity_in_days": 2,
                        "multiple_clubs": false
                        "club": {
                            "credit_left": 12,
                            "subscription_name": "Maandabonnement - onbeperkt",
                            "subscription_date_start": "2015-02-11T00:00:00+0100",
                            "subscription_date_end": "2016-02-01T00:00:00+0100",
                            "subscription_payment_due": false,
                            "last_activity": "2015-08-04T19:30:00+0100"
                        }
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
                        "name": "Lode Claassen",
                        "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                        "phone": "",
                        "activities_done": 2,
                        "last_activity_in_days": 40,
                        "multiple_clubs": false
                    },
                    "relationships": {
                        "club": {
                            "data": {
                                "type": "club",
                                "id": 42
                            }
                        }
                    },
                    "links": {
                        "registered_activities": "/users/registrations",
                        "following_activities": "/users/followings",
                        "giving_activities": "/users/activities"
                    }
                },
                "included": [
                    {
                        "type": "club",
                        "id": 42,
                        "attributes": {
                            "name": "OUT!-Sport",
                            "logo": "https://dxltue5g50eu3.cloudfront.net/content/icons/1/logo%20OUT!%20met%20url.png"
                        },
                        "links": {
                            "self": "/clubs/42",
                            "members": "/clubs/42/members"
                        }
                    }
                ],
                "meta": {
                    "interface_type": "trainer"
                }
            }
