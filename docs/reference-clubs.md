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
                        "club_detail": "/api/clubs/{club_id}"
                    }
                }
            }

## Clubs item [/clubs/{club_id}]

Information about the club of an activity.

+ name
+ logo
+ description
+ activities
    + id

+ Parameters
    + club_id (required, number, `42`) ... ID of the Club

### View a club detail [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/clubs/42/"
                },
                "data": {
                    "type": "club",
                    "id": 42,
                    "attributes": {
                        "name": "OUT!-Sport",
                        "logo": "https://dxltue5g50eu3.cloudfront.net/content/icons/1/logo%20OUT!%20met%20url.png",
                        "description": "Zoek je een superleuke en goede buitensporttraining voor de laagst mogelijke prijs? Wat jij wilt: ..."
                    },
                    "relationships": {
                        "activities": {
                            "data": { "type": "activity", "id": [ 42, 24 ] }
                        }
                    },
                    "links": {
                        "self": "/clubs/42/",
                        "members": "/clubs/42/members"
                    }
                }
            }

## Club members collection [/clubs/{club_id}/members]

This is only available for trainers.

+ name
+ avatar
+ phone
+ club
    + credit_left
    + subscription_name
    + subscription_date_start
    + subscription_date_end
    + subscription_payment_due
    + last_activity

+ Parameters
    + club_id (required, number, `42`) ... ID of the Club

### Lists all members [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/clubs/42/members"
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
                                "self": "/clubs/42/members/42"
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
                        "name": "Lode Claassen",
                        "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                        "phone": "",
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
                        "self": "/clubs/42/members/42"
                    }
                }
            }

## Club member [/clubs/{club_id}/members/{user_id}]

+ name
+ avatar
+ phone
+ club
    + credit_left
    + subscription_name
    + subscription_date_start
    + subscription_date_end
    + subscription_payment_due
    + last_activity

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
                        "name": "Lode Claassen",
                        "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                        "phone": "",
                        "club": {
                            "credit_left": 12,
                            "subscription_name": "Maandabonnement - onbeperkt",
                            "subscription_date_start": "2015-02-11T00:00:00+0100",
                            "subscription_date_end": "2016-02-01T00:00:00+0100",
                            "subscription_payment_due": true,
                            "last_activity": "2015-08-04T19:30:00+0100"
                        }
                    },
                    "links": {
                        "self": "/clubs/42/members/42"
                    }
                }
            }
