FORMAT: 1A

#InteractAPI

The Interact API provide programmatic access to read and write Interact's data.
You can get and interact with the whole data...
It identifies Interact applications and users using OAuth2.
Responses are available in JSON.

## Specifications

The API works over the https protocol.
```no-highlight
The current endpoint is https://api.nova.interact.objectivemoon.io/docs
All data is sent and received as JSON.
```
## Authentication

The authentication on the InterAct API works with OAuth2.

OAuth2 is a protocol that lets external apps request authorization to details in a user’s InterAct App without getting their password.
This is preferred over a basic authentication because tokens can be limited to specific types of data, and can be revoked by users at any time.

All developers need to register their application before getting started. 
A registered OAuth application is assigned a unique Client ID and Client Secret.
The Client Secret should not be shared.

### Register your application

#### Visit this website to register your app:
```no-highlight
https://api.nova.interact.objectivemoon.io
```

Complete the form to get a `client_id` and a private `client_secret`.

Now, to connect yours users, insert in your app a link to
```no-highlight
https://api.nova.interact.objectivemoon.io/auth/interact_oauth2/authorize?client_id=`your_client_id`
```
This `GET` action redirect users to a registration or sign in form. Once the user completed form, the callback uri is called. You will receive a `code` 

## Upload Applications [/applications/upload]

### Upload Application [POST]

Upload application.

* **name**: `MyApp` (string, optional) - The nane of your app
* **group_id**: `[8940]` (array, optional) - Application's groups ids
* **catchphrase**: `The best app` (string, optional) - Application's catch phrase
* **description**: `Never miss a deal` (string, optional) - Application's description
* **icon**: icon.png (attachement, optional) - Application's icon
* **banner**: file (attachement, optional) - Application's banner
* **screenshot1**: file1.png (attachement, optional) - Application's screenshot 1
* **screenshot2**: file2.png (attachement, optional) - Application's screenshot 2
* **screenshot3**: file3.png (attachement, optional) - Application's screenshot 3
* **screenshot4**: file4.png (attachement, optional) - Application's screenshot 4
* **screenshot5**: file5.png (attachement, optional) - Application's screenshot 5

+ Attributes
    + application (object)
        + binary_path: "http://www.application.io/application.ipa" (string, required) - Application's binary url
        + screenshot1: "http://www.application.io/screenshot1.png" (string, optional) - Application's screenshot 1 url
        + screenshot2: "http://www.application.io/screenshot2.png" (string, optional) - Application's screenshot 2 url
        + screenshot3: "http://www.application.io/screenshot3.png" (string, optional) - Application's screenshot 3 url
        + screenshot4: "http://www.application.io/screenshot4.png" (string, optional) - Application's screenshot 4 url
        + screenshot5: "http://www.application.io/screenshot5.png" (string, optional) - Application's screenshot 5 url
        + banner: "http://www.application.io/banner.png" (string, optional) - Application's banner url
        + description: "Never miss a deal" (string, optional) - Application's description
        + catchphrase: "The best app" (string, optional) - Application's catchphrase

+ Request
    + Headers

            Content-Type: application/json

    + Body

              {
                  "application": {
                      "binary_path": "http://www.application.io/application.ipa",
                      "screenshot1": "http://www.application.io/screenshot1.png",
                      "screenshot2": "http://www.application.io/screenshot2.png",
                      "screenshot3": "http://www.application.io/screenshot3.png",
                      "screenshot4": "http://www.application.io/screenshot4.png",
                      "screenshot5": "http://www.application.io/screenshot5.png",
                      "banner": "http://www.application.io/banner.png",
                      "description": "Never miss a deal",
                      "catchphrase": "The best app"
                    }
              }

+ Response 201 (application/json)


    + Body

              {
                  "status" : "Binary processing", "link":"https://www.appaloosa-store.com/api/v1/52/applications/123?api_key=yourapikey"
              }

