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
+ status (enum joins|cancelled)
+ presence (enum unknown|present|absent)
+ subscription_payment_due

+ Parameters
    + activity_id (required, number, `42`) ... ID of the Activity

### Get the participants of an activity [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities/42/participants"
                    "activity_details": "/activities/42"
                },
                "data":
                    [
                        {
                            "type": "user",
                            "id": 42,
                            "attributes": {
                                "name": "Niels Groen",
                                "avatar": "sportyguru78.jpg",
                                "status": "joins",
                                "presence": "unknown",
                                "subscription_payment_due": false,
                            },
                            "links": {
                                "self": "/activities/42/participant/42"
                            }
                        }
                    ]
            }

## Activity participant [/activities/{activity_id}/participants/{user_id}]

+ name
+ avatar
+ phone
+ status (enum joins|cancelled)
+ presence (enum unknown|present|absent)
+ subscription_payment_due
+ subscription_credits_left
+ subscription_start
+ subscription_end
+ subscription_method
+ subscription_club

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
                    "participants": "/activities/42/participants"
                    "activity_details": "/activities/42"
                },
                "data": {
                    "type": "user",
                    "id": 42,
                    "attributes": {
                        "name": "Niels Groen",
                        "avatar": "sportyguru78.jpg",
                        "phone": "06 - 12 34 56 78",
                        "status": "joins",
                        "presence": "unknown",
                        "subscription_payment_due": false,
                        "subscription_credits_left": 9,
                        "subscription_start": "2015-05-12",
                        "subscription_end": "2015-06-12",
                        "subscription_method": "Abonnement",
                    },
                    "links": {
                        "self": "/activities/42/participant/42",
                        "presence": "/activities/42/participant/42/presence",
                        "subscription_club": {
                            "related": "/clubs/42",
                            "linkage": { "type": "club", "id": 42 }
                        },
                    }
                },
                "included": [
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
                ],
                "meta": {
                    "messages": {
                        "subscription_payment_due": "Betalingsachterstand"
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
