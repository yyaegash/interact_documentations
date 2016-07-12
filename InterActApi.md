FORMAT: 1A

#InteractAPI

The Interact API provide programmatic access to read and write Interact’s data. You can get and exchange It identifies Interact applications and users using OAuth2. Request and responses are in JSON.

## Specifications
- The API works over the https protocol.
- All data is sent and received as JSON.

The root application is: 
```no-highlight
https://interact.objectivemoon.io/
```

The current endpoint is
```no-highlight
https://interact.objectivemoon.io/docs
```

## Authentication
The authentication on the InterAct API works with OAuth2.

OAuth2 is a protocol that lets external apps request authorization to details in a user’s InterAct App without getting their password. This is preferred over a basic authentication because tokens can be limited to specific types of data, and can be revoked by users at any time.

All developers need to register their application before getting started. A registered OAuth application is assigned a unique Client ID and Client Secret. The Client Secret should not be shared.


## Register your application

First of all visit this page to register your app:

#### Visit this website to register your app:
```no-highlight
https://dashboard.interact.objectivemoon.io/
```

Complete the entire form to get a `client_id` and a private `client_secret`.

Now, to connect yours users, call this link:

```no-highlight
https://interact.objectivemoon.io/auth/interact_oauth/authorize?client_id=`your_client_id`
```


This `GET` action redirect users to a registration or sign in form. Once the user completed form, the callback uri is called. You will receive a `code` 

# Group OAuth

## Authorize [/auth/interact_oauth/authorize]
This `POST` action redirect user to a sign-in or sign-up form. Once the user completed form, the callback uri is called and you will receive a `code`. This code allow you to get the user token.

### Authorize [POST]

* **client_id**: `d59bc5349760bb8d917e711a9efed206` (string, required) - Your client id
* **client_decret**: `202ef84e2323439a5a5dcdd74bd5a994` (string, required) - Your client secret

+ Attributes
    + auth (object)
        + client_id: "d59bc5349760bb8d917e711a9efed206" (string, required) - Your client id
        + client_secret: "202ef84e2323439a5a5dcdd74bd5a994" (string, required) - Your client secret

+ Request
    + Headers

            Content-Type: application/json

    + Body

              {
                  "auth": {
                      "client_id": "d59bc5349760bb8d917e711a9efed206",
                      "client_secret": "202ef84e2323439a5a5dcdd74bd5a994"
                    }
              }

## Access Token [/auth/interact_oauth/access_token]
### Access Token [POST]
Save the `token`, it’s will be asked for the next requests.

* **client_id**: `d59bc5349760bb8d917e711a9efed206` (string, required) - Your client id
* **client_decret**: `202ef84e2323439a5a5dcdd74bd5a994` (string, required) - Your client secret
* **code**: `d657ca129bb18a06247f6d80f1390725` (string, required) - The code received

+ Attributes
    + auth (object)
        + client_id: "d59bc5349760bb8d917e711a9efed206" (string, required) - Your client id
        + client_secret: "202ef84e2323439a5a5dcdd74bd5a994" (string, required) - Your client secret
        + code: "d657ca129bb18a06247f6d80f1390725" (string, required) - The code received

+ Request
    + Headers

            Content-Type: application/json

    + Body

              {
                  "auth": {
                      "client_id": "d59bc5349760bb8d917e711a9efed206",
                      "client_secret": "202ef84e2323439a5a5dcdd74bd5a994",
                      "code": "d657ca129bb18a06247f6d80f1390725"
                    }
              }

+ Response 200 
    + Body

              {
                "token": "4a2984bdc5c1f559fa86ca633d899f9039a0",
                "token_type": "bearer",
                "uid": f90ad4,
                "info": {
                  "email": "user.email@demo.com"
                }
              }

# Group Data
## Store Data [/api/v1/data]
### Create Data [POST]
Create data from your user.

* **client_id**: `d59bc5349760bb8d917e711a9efed206` (string, required) - Your client id
* **client_decret**: `202ef84e2323439a5a5dcdd74bd5a994` (string, required) - Your client secret
* **user_token**: `4a2984bdc5c1f559fa86ca633d899f9039a0` (string, required) - The user token received
* **data**: `{}` (hash, required) - User data, the key belongs to keyword collection, and value is an hash of keyword's fields


+ Attributes
    + data (object)
        + client_id: "d59bc5349760bb8d917e711a9efed206" (string, required) - Your client id
        + client_secret: "202ef84e2323439a5a5dcdd74bd5a994" (string, required) - Your client secret
        + user_token: "4a2984bdc5c1f559fa86ca633d899f9039a0" (string, required) - The user token received
        + data: "{'key': 'value'}" (object, required) - `key` belongs to Keword collection and `value` belongs to `keyword`

+ Request
    + Headers

            Content-Type: application/json

    + Body

              {
                  "data": {
                      "client_id": "d59bc5349760bb8d917e711a9efed206",
                      "client_secret": "202ef84e2323439a5a5dcdd74bd5a994",
                      "user_token": "4a2984bdc5c1f559fa86ca633d899f9039a0",
                      "data": {
                        "typo": { 
                          "typo": 1,
                          "duration": 12
                        }
                      }
                    }
              }

+ Response 201 

    + Body
              [
                  {
                      "key": "typo",
                      "payload": {
                          "typo": 1,
                          "duration": 12,
                          "created_at": "2016-06-01 23:25:23 +0200",
                      }
                  }
              ]

## Get user actions [/api/v1/data/user_actions]
### Create Data [POST]
Collect all actions from specific user

* **client_id**: `d59bc5349760bb8d917e711a9efed206` (string, required) - Your client id
* **client_decret**: `202ef84e2323439a5a5dcdd74bd5a994` (string, required) - Your client secret
* **user_token**: `4a2984bdc5c1f559fa86ca633d899f9039a0` (string, required) - The user token received

+ Attributes
    + client_id: "d59bc5349760bb8d917e711a9efed206" (string, required) - Your client id
    + client_secret: "202ef84e2323439a5a5dcdd74bd5a994" (string, required) - Your client secret
    + data (object)
        + user_token: "4a2984bdc5c1f559fa86ca633d899f9039a0" (string, required) - The user token received

+ Request
    + Headers

            Content-Type: application/json

    + Body

              {
                  "client_id": "d59bc5349760bb8d917e711a9efed206",
                  "client_secret": "202ef84e2323439a5a5dcdd74bd5a994"
                  "data": {
                      "user_token": "4a2984bdc5c1f559fa86ca633d899f9039a0"
                    }
              }

+ Response 200

    + Body
        {
            "user_actions": [
                {
                    "key": "sleep_time",
                    "payload": [
                        {
                            "duration": "12h30",
                            "started_at": "2016-06-01 23:25:23 +0200",
                            "ended_at": "2016-06-02 07:01:30 +0200"
                        },
                        {
                            "duration": "9h30",
                            "started_at": "2016-06-01 13:25:23 +0200",
                            "ended_at": "2016-06-02 09:16:30 +0200"
                        }
                    ]
                },
                {
                    "key": "sleep_quality",
                    "payload": {
                        "quality": "good"
                    }
                },
                {
                    "key": "typo",
                    "payload": {
                        "typo": 1,
                        "duration": 12,
                        "created_at": "2016-06-01 23:25:23 +0200",
                    }
                }
            ]
        }


# Get user actions [/api/v1/data/aggregate_actions]
### Retrieve Data [POST]
Return 30 records randomly selected. All requests below 10 records could not be rendered. query parameter could be an array or a string params

* **query**:  (array, required) - The query

+ Request
    + Headers

            Content-Type: application/json

    + Body

          {
              "data": {
                      "query": [
                          {
                              "key": "typo",
                              "where": [
                                  {
                                      "range": { "sentence_length":  [40, 50]  }
                                  },
                                  {
                                      "egal": { "done": true }
                                  }
                              ],
                              "where_not": []
                          },{
                              "key": "education",
                              "where": [
                                  { 
                                      "egal": {
                                          "specialized_school": true
                                      }
                                  }
                              ]
                          }
                      ]
                  }
          }

+ Response 200

      + Body

            {
            "aggregate_actions": [
              {
                "key": "typo",
                "payload": {
                  "sentence_length": 50,
                  "sentence": "Ex itaque nostrum fugit distinctio ea consectetur.",
                  "typo": 7,
                  "duration": 3,
                  "done": true,
                  "event_at": false
                }
              },
              {
                "key": "typo",
                "payload": {
                  "sentence_length": 43,
                  "sentence": "Quos quibusdam cumque excepturi libero sit.",
                  "typo": 1,
                  "duration": 6,
                  "done": true,
                  "event_at": true
                }
              },
              {
                "key": "typo",
                "payload": {
                  "sentence_length": 50,
                  "sentence": "Maiores sit officia aspernatur at aut et voluptas.",
                  "typo": 5,
                  "duration": 10,
                  "done": true,
                  "event_at": true
                }
              }
            }