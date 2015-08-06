FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# Group Clubs

Resources for getting information about a club.

## Club endpoints [/clubs]

## Get possible endpoints [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/clubs"
                },
                "data": [],
                "meta": {
                    "endpoints": {
                        "club_detail": "/clubs/{club_id}"
                    }
                }
            }

## Clubs item [/clubs/{club_id}]

Information about the club of an activity.

+ name
+ logo

+ Parameters
    + club_id (required, number, `42`) ... ID of the Club

### View a club detail [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/clubs/42",
                    "members": "/clubs/{club_id}/members",
                },
                "data": {
                    "type": "club",
                    "id": 42,
                    "attributes": {
                        "name": "Calandfit",
                        "logo": "calandfit.png"
                    },
                    "links": {
                        "self": "/clubs/42",
                        "activities": {
                            "linkage": { "type": "activity", "id": [42,24,44,22] }
                        }
                    }
                }
            }

## Club members collection [/clubs/{club_id}/members]

This is only available for trainers.

+ name
+ avatar
+ subscription_payment_due

+ Parameters
    + club_id (required, number, `42`) ... ID of the Club

### Lists all members [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/club/42/members"
                    "club_details": "/club/42"
                },
                "data":
                    [
                        {
                            "type": "user",
                            "id": 42,
                            "attributes": {
                                "name": "Niels Groen",
                                "avatar": "sportyguru78.jpg",
                                "subscription_payment_due": false,
                            },
                            "links": {
                                "self": "/activities/42/members/42"
                            }
                        }
                    ]
            }

### Add a new member [POST]

Adds a person as member of the club.

Mostly, unregistered users are members of the club and are listed on above endpoint.
POSTing to this endpoint allows the trainer to add a new user as a member.

The trainer can then register them to the activity and mark their presence.

+ emailaddress (string) - Email address of the person

+ Request (application/json)

            {
                "emailaddress": "john@doe.com",
            }

+ Response 201 (application/json)

    + Headers

            Location: /clubs/42/members/42

    + Body

            {
                "links": {
                    "self": "/activities/42/members/42"
                },
                "data": {
                    "type": "user",
                    "id": 42,
                    "attributes": {
                        "name": "Niels Groen",
                        "avatar": "sportyguru78.jpg",
                        "phone": "06 - 12 34 56 78",
                        "subscription_payment_due": false,
                        "subscription_credits_left": 9,
                        "subscription_start": "2015-05-12",
                        "subscription_end": "2015-06-12",
                        "subscription_method": "Abonnement",
                    },
                    "links": {
                        "self": "/activities/42/members/42"
                    }
                },
                "meta": {
                    "messages": {
                        "subscription_payment_due": "Betalingsachterstand"
                    }
                }
            }

## Club member [/clubs/{club_id}/members/{user_id}]

+ name
+ avatar
+ phone
+ subscription_payment_due
+ subscription_credits_left
+ subscription_start
+ subscription_end
+ subscription_method
+ subscription_club

+ Parameters
    + club_id (required, number, `42`) ... ID of the Club
    + user_id (required, number, `42`) ... ID of the Member

### View a member detail [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/activities/42/members/42"
                },
                "data": {
                    "type": "user",
                    "id": 42,
                    "attributes": {
                        "name": "Niels Groen",
                        "avatar": "sportyguru78.jpg",
                        "phone": "06 - 12 34 56 78",
                        "subscription_payment_due": false,
                        "subscription_credits_left": 9,
                        "subscription_start": "2015-05-12",
                        "subscription_end": "2015-06-12",
                        "subscription_method": "Abonnement",
                    },
                    "links": {
                        "self": "/activities/42/members/42"
                    }
                },
                "meta": {
                    "messages": {
                        "subscription_payment_due": "Betalingsachterstand"
                    }
                }
            }
