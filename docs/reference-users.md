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

### View currently logged in trainer [GET]

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

## User device [/users/device]

(De-)Activating a mobile device for the current user.
This allows for push notifications to be sent to the user's device.

Right now only Android and iOS devices are recognized.

### (Re-)Activate a device [PUT]

Using PUT activates the device, or marks it as still active when already activated.
Use this when logging in after asking the users permission.

We allow multiple devices per user but only send push notifications to the latest one.
To facilitate this, call this endpoint every time the user (re-)opens the app.
The device which opened the app the last will receive the push notifications.

+ device (required, string, `Android`) ... Type of the device: either `Android` or `iOS`
+ identifier (required, string, `Zan63Ru7ABuk4nuwRus6ubr5SPuzesab`) ... The id of the device

+ Request (application/json)

            {
                "device": "Android",
                "identifier": "Zan63Ru7ABuk4nuwRus6ubr5SPuzesab"
            }

+ Response 204 (application/json)

### De-activate a device [DELETE]

Using DELETE de-activates the device, stopping push notifications.
Use this when logging out of the app to allow multiple users using a single device.

It would be good to offer users a way to disable notifications while logged in as well.

After de-activating, the user will continue to receive notifications via email.

+ device (required, string, `Android`) ... Type of the device: either `Android` or `iOS`
+ identifier (required, string, `Zan63Ru7ABuk4nuwRus6ubr5SPuzesab`) ... The id of the device

+ Request (application/json)

            {
                "device": "Android",
                "identifier": "Zan63Ru7ABuk4nuwRus6ubr5SPuzesab"
            }

+ Response 204 (application/json)

## Test notification [/users/testnotification]

Send a push notification to the [user's registered device](/reference/users/user-device).

This is mainly meant for development purposes.

### Send a push notification as test [POST]

You'll receive an empty response body from the API, and the push notification at the device.
Note this only works if you registered the user's device.

+ type (optional, string, `new-message`) ... Type of the message: one of `test`, `new-message`, `cancelled-activity`, `restored-activity`

+ Request (application/json)

            {
                "type": "new-message"
            }

+ Response 204 (application/json)
