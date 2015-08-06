FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# Group Trainers

Resources for getting information about a trainer.

## Trainer endpoints [/trainers]

## Get possible endpoints [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/trainers"
                },
                "data": [],
                "meta": {
                    "endpoints": {
                        "trainer_detail": "/trainers/{trainer_id}"
                    }
                }
            }

## Trainer item [/trainers/{user_id}]

Information about the trainer of an activity.

+ name
+ avatar
+ phone
+ email
+ introduction
+ club
    + name
    + logo
+ activities
    + id

+ Parameters
    + user_id (required, number, `42`) ... ID of the Trainer

### View a trainer detail [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/trainers/42"
                },
                "data": {
                    "type": "user",
                    "id": 42,
                    "attributes": {
                        "name": "Vincent Van den Tol",
                        "avatar": "https://dxltue5g50eu3.cloudfront.net/content/profile/1/558077f02c968_photo.JPG",
                        "phone": "",
                        "email": "vincent@alsvanzelf.nl",
                        "introduction": ""
                    },
                    "relationships": {
                        "club": {
                            "links": { "related": "/club/42" },
                            "data": { "type": "club", "id": 42 }
                        },
                        "activities": {
                            "data": { "type": "activity", "id": [ 42, 24 ] }
                        }
                    },
                    "links": {
                        "self": "/trainers/42"
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
                            "self": "/clubs/42"
                        }
                    }
                ]
            }
