FORMAT: 1A
HOST: http://docs.out2move.apiary.io/

# Group Conversations

Conversations between trainers and their participants.

Each conversations is connected to a club.
Conversations are only visible if you are connected to the club.

- A sportsman only sees conversations from clubs they follow.
- A trainer only sees conversations from clubs they train at.
  Note, a trainer *does not* see conversations from clubs they follow themselves.

For now, conversations are initiated one-way, only trainers can start them.
Participants can add messages inside a conversation.

For now, (un)read status is *not* tracked for conversations or messages.
Clients should build an own cache of the (un)read status.

## Conversations collection [/conversations{?club_id}]

+ title
+ starting_date
+ total_message_count
+ last_message_date
+ author
    + name
    + avatar
    + phone
+ starting_message
    + text
    + date

+ Parameters
    + club_id (optional, number, `42`) ... To only select conversations from that club

### Lists all conversations [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/conversations"
                },
                "data":
                    [
                        {
                            "type": "conversation",
                            "id": 42,
                            "attributes": {
                                "title": "Welkom",
                                "starting_date": "2015-06-23T14:15:38+0200"
                            },
                            "relationships": {
                                "author": {
                                    "data": { "type": "user", "id": 42 }
                                },
                                "starting_message": {
                                    "data": { "type": "message", "id": 42 }
                                }
                            },
                            "links": {
                                "self": "/conversations/42"
                            }
                        }
                    ],
                "included":
                    [
                        {
                            "type": "user",
                            "id": 42,
                            "attributes": {
                                "name": "Lode Claassen",
                                "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                                "phone": ""
                            }
                        },
                        {
                            "type": "message",
                            "id": 42,
                            "attributes": {
                                "text": "Aan iedereen natuurlijk!",
                                "date": "2015-06-23T14:15:38+0200"
                            }
                        }
                    ]
            }

### Add a new conversation [POST]

By starting a conversation with a `message` parameter, a push notification is sent out.
See [adding a message](/reference/conversations/message-collection) for details.

+ club_id (required, number, `42`) ... The club the conversation belongs to
+ title (optional, string) - Title of the conversation
+ message (optional, string) - First message in the conversation

+ Request (application/json)

            {
                "club_id": 42,
                "title": "Welkom",
                "message": "Aan iedereen natuurlijk!",
            }

+ Response 201 (application/json)

    + Headers

            Location: /conversations/42

    + Body

            {
                "links": {
                    "self": "/conversations/42"
                },
                "data": {
                    "type": "conversation",
                    "id": 42,
                    "attributes": {
                        "title": "Welkom",
                        "starting_date": "2015-06-23T14:15:38+0200"
                    },
                    "relationships": {
                        "author": {
                            "data": { "type": "user", "id": 42 }
                        },
                        "starting_message": {
                            "data": { "type": "message", "id": 42 }
                        }
                    },
                    "links": {
                        "self": "/conversations/42",
                        "messages": "/conversations/42/messages"
                    }
                },
                "included":
                    [
                        {
                            "type": "user",
                            "id": 42,
                            "attributes": {
                                "name": "Lode Claassen",
                                "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                                "phone": "",
                            }
                        },
                        {
                            "type": "message",
                            "id": 42,
                            "attributes": {
                                "text": "Aan iedereen natuurlijk!",
                                "date": "2015-06-23T14:15:38+0200"
                            }
                        }
                    ]
            }

## Conversation item [/conversations/{conversation_id}]

+ title
+ starting_date
+ author
    + name
    + avatar
    + phone
+ starting_message
    + text
    + date

+ Parameters
    + conversation_id (required, number, `42`) ... ID of the Conversation

### View details of a conversation [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/conversations/42"
                },
                "data": {
                    "type": "conversation",
                    "id": 42,
                    "attributes": {
                        "title": "Welkom",
                        "starting_date": "2015-06-23T14:15:38+0200"
                    },
                    "relationships": {
                        "author": {
                            "data": { "type": "user", "id": 42 }
                        },
                        "starting_message": {
                            "data": { "type": "message", "id": 42 }
                        }
                    },
                    "links": {
                        "self": "/conversations/42",
                        "messages": "/conversations/42/messages"
                    }
                },
                "included":
                    [
                        {
                            "type": "user",
                            "id": 42,
                            "attributes": {
                                "name": "Lode Claassen",
                                "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                                "phone": "",
                            }
                        },
                        {
                            "type": "message",
                            "id": 42,
                            "attributes": {
                                "text": "Aan iedereen natuurlijk!",
                                "date": "2015-06-23T14:15:38+0200"
                            }
                        }
                    ]
            }

## Message collection [/conversations/{conversation_id}/messages]

+ text
+ date
+ author
    + name
    + avatar
    + phone

+ Parameters
    + conversation_id (required, number, `42`) ... ID of the Conversation

### Lists all messages [GET]

+ Response 200 (application/json)

    + Body

            {
                "links": {
                    "self": "/conversations/42/messages"
                },
                "data":
                    [
                        {
                            "type": "message",
                            "id": 42,
                            "attributes": {
                                "text": "Aan iedereen natuurlijk!",
                                "date": "2015-06-23T14:15:38+0200"
                            },
                            "relationships": {
                                "author": {
                                    "data": { "type": "user", "id": 42 }
                                }
                            }
                        },
                        {
                            "type": "message",
                            "id": 44,
                            "attributes": {
                                "text": "Thanks!",
                                "date": "2015-06-23T14:16:50+0200"
                            },
                            "relationships": {
                                "author": {
                                    "data": { "type": "user", "id": 24 }
                                }
                            }
                        }
                    ],
                "included":
                    [
                        {
                            "type": "user",
                            "id": 42,
                            "attributes": {
                                "name": "Lode Claassen",
                                "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                                "phone": "",
                            }
                        },
                        {
                            "type": "user",
                            "id": 24,
                            "attributes": {
                                "name": "Vincent Van den Tol",
                                "avatar": "https://dxltue5g50eu3.cloudfront.net/content/profile/1/558077f02c968_photo.JPG",
                                "phone": ""
                            }
                        }
                    ]
            }

### Add a new message [POST]

By adding a message, a push notification is sent out to all other members and trainers of the club.
The metadata of the push notification will contain a `type` of `new-message`.
Further it contains a `message_id` and `conversation_id` to redirect users to a relevant place.

+ conversation_id (required, number, `42`) ... The conversation to add the message to
+ message (string) - Contents of the new message

+ Request (application/json)

            {
                "message": "Thanks :)",
            }

+ Response 201 (application/json)

    + Headers

            Location: /conversations/42/messages

    + Body

            {
                "links": {
                    "self": "/conversations/42/messages"
                },
                "data":
                    [
                        {
                            "type": "message",
                            "id": 42,
                            "attributes": {
                                "text": "Aan iedereen natuurlijk!",
                                "date": "2015-06-23T14:15:38+0200"
                            },
                            "relationships": {
                                "author": {
                                    "data": { "type": "user", "id": 42 }
                                }
                            }
                        },
                        {
                            "type": "message",
                            "id": 44,
                            "attributes": {
                                "text": "Thanks!",
                                "date": "2015-06-23T14:16:50+0200"
                            },
                            "relationships": {
                                "author": {
                                    "data": { "type": "user", "id": 24 }
                                }
                            }
                        }
                    ],
                "included":
                    [
                        {
                            "type": "user",
                            "id": 42,
                            "attributes": {
                                "name": "Lode Claassen",
                                "avatar": "http://www.out2move.nl/assets/img/icons/anonymous.jpg",
                                "phone": "",
                            }
                        },
                        {
                            "type": "user",
                            "id": 24,
                            "attributes": {
                                "name": "Vincent Van den Tol",
                                "avatar": "https://dxltue5g50eu3.cloudfront.net/content/profile/1/558077f02c968_photo.JPG",
                                "phone": ""
                            }
                        }
                    ]
            }
