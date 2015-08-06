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

+ Parameters
    + user_id (required, number, `42`) ... ID of the Trainer

### View a trainer detail [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/trainers/42",
                },
                "data": {
                    "type": "user",
                    "id": 42,
                    "attributes": {
                        "name": "Pavlov van Beerkoop",
                        "avatar": "pavlov.jpg",
                        "phone": "06 123 456 78",
                        "email": "pavlov@beerkooptraining.nl",
                        "introduction": "Trailrunning is hardlopen in de natuur. ..."
                    },
                    "links": {
                        "self": "/trainers/42",
                        "club": {
                            "related": "/clubs/42",
                            "linkage": { "type": "club", "id": 42 }
                        },
                        "activities": {
                            "linkage": { "type": "activity", "id": [42,24,44,22] }
                        }
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
                ]
            }
