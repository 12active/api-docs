FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# Group Participants

Resources with information about participants of activities.

This is only available for trainers.
Participants can update their own registration for a specific activity via the [activity registration endpoint](/reference/activities/activity-registration).

## Activity participants collection [/activities/{activity_id}/participants]

Lists people who join(ed) an activity.

+ name
+ avatar
+ phone
+ activity
    + status (enum joins|cancelled)
    + presence (enum unknown|present|absent)
+ club
    + credit_left
    + subscription_name
    + subscription_date_start
    + subscription_date_end
    + subscription_payment_due
    + last_activity

+ Parameters
    + activity_id (required, number, `42`) ... ID of the Activity

### Get the participants of an activity [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities/42/participants"
                },
                "data":
                    [
                        {
                            "type": "user",
                            "id": 42,
                            "attributes": {
                                "name": "Lode Claassen",
                                "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                                "phone": "",
                                "activity": {
                                    "status": "joins",
                                    "presence": "present"
                                },
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
                                "self": "/activities/42/participants/42"
                            }
                        }
                    ]
            }

## Activity participant [/activities/{activity_id}/participants/{user_id}]

+ name
+ avatar
+ phone
+ activity
    + status (enum joins|cancelled)
    + presence (enum unknown|present|absent)
+ club
    + credit_left
    + subscription_name
    + subscription_date_start
    + subscription_date_end
    + subscription_payment_due
    + last_activity

+ Parameters
    + activity_id (required, number, `42`) ... ID of the Activity
    + user_id (required, number, `42`) ... ID of the Participant

### Add a user as participant [POST]

Add a user as a participant of the activity.

Normally, the user registers by them self.
This endpoint allows the trainer to register a unregistered participant.
The participant receive a notification as it impacts payments.

A trainer can only add users which are members of the club.
To get a user id for the request, fetch a list of members via the [club members endpoint](/reference/clubs/club-members-collection).

+ Response 204 (application/json)

    + Headers

            Location: /activities/42/participants/42

### View a participant detail [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities/42/participants/42"
                },
                "data": {
                    "type": "user",
                    "id": 42,
                    "attributes": {
                        "name": "Lode Claassen",
                        "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                        "phone": "",
                        "activity": {
                            "status": "joins",
                            "presence": "present"
                        },
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
                        "self": "/activities/42/participants/42"
                    }
                }
            }

## Participant presence [/activities/{activity_id}/participants/{user_id}/presence]

Marking a participant as present finishes the payment loop.
Marking as absent, allows for a refund in some subscriptions.

+ Parameters
    + activity_id (required, number, `42`) ... ID of the Activity
    + user_id (required, number, `42`) ... ID of the Participant

### Mark a participant as present [PUT]

Using PUT marks the participant as present.
Make the request without a request body.

+ Response 204 (application/json)

    + Headers

            Location: /activities/42/participants/42

### Mark a participant as absent [DELETE]

Using DELETE marks the participant as absent.
Make the request without a request body.

+ Response 204 (application/json)

    + Headers

            Location: /activities/42/participants/42
