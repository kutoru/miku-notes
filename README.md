# What is Miku Notes?

The app allows multiple users to store and manage personal [*notes*](#features) and [*shelves*](#features). The application's backend is supposed to be self-hosted, and the frontend is available in the form of both a web app and an Android app.

**Note** that the main purpose of this project is more about exploring and learning how real-world projects could work, and less about being an actual usable application. With having that said, once the **Frontend** is done, it should in theory be a proper application, and perhaps in the future we might expand it into something like a self-hosted cloud storage for all of your files, notes, memos, todos and other things like that.

## Features

*Notes* themselves don't have any special features yet, and for now the app allows users to create/edit/delete them, as well as attach/detach any files and *tags* to individual notes. The *notes* can be ordered and filtered, and *tags* come in handy when users might need to group certain notes together by filtering them.

*Shelves* are kind of similar to *notes*, in a sense that users can store text and files in them, but they are supposed to be easier to access, use and dispose of. Think of them like temporary one-time *notes*. Each user can have exactly one *shelf*, and it is available in the frontend's main page. The *shelves* might be useful when users need to store something like a little temporary memo, that they plan on deleting soon, or perhaps when users need to quickly share some files or text between their devices.

## Structure

This app consists of five main parts, three microservices and two frontends:
- [Auth service](https://github.com/kuromii5/miku-notes-auth), which is responsible for managing user accounts, as well as the main user authentication logic.
- [Data service](https://github.com/kutoru/miku-notes-data), which is responsible for managing user-generated data, such us the *notes* and the *shelves* mentioned above.
- [Gateway service](https://github.com/kutoru/miku-notes-gateway), which exposes the application's API by acting as a layer between the other two services and the frontends.
- [Frontend](https://github.com/kinokorain/miku-notes-frontend), which is the web frontend for the app.
- [Android frontend](https://github.com/kutoru/miku-notes-android), which is the native Android frontend for the app.

# How to run it locally?

The best way to run the app is with Docker by using `docker compose up` in the root directory. If you are using the default [configuration](#env), then after successful launch, the app's API should be available at `http://localhost:3030`. **Note** that since the frontends aren't yet fully functional, the only way to properly try out this app is through its API. The API's documentation should be available at `http://localhost:3030/swagger-ui`.

You could also run the services manually without Docker. To do so, you should go into each service's repository and explore the readmes there.

To run the Android application, visit its [releases](https://github.com/kutoru/miku-notes-android/releases), download and install the latest one. Alternatively, you could also clone the repo and build the APK yourself.

# .env

An example .env configuration is included in the repository, and the application should work just fine with the default values specified there. But if for whatever reason you want to modify the configuration, here are the explanations for each field:

Database:
- `DB_NAME`: name for the database
- `DB_PASS`: password for the database user
- `DB_USER`: username for the database user

Auth service:
- `AUTH_SERVICE_ENV`: environment for the service that acts as a log level. Can either be `dev`, `prod` or `local`
- `AUTH_SERVICE_SECRET`: secret that will be used to encrypt and decrypt JWTs (which are used as access tokens)
- `AUTH_SERVICE_PORT`: port that this service will run on
- `AUTH_SERVICE_TOKEN`: token that will be used to validate incoming requests to this service

Data service:
- `DATA_SERVICE_PORT`: port that this service will run on
- `DATA_SERVICE_TOKEN`: token that will be used to validate incoming requests to this service

Gateway service:
- `GATEWAY_SERVICE_LOG_LEVEL`: log level for this service. Can either be `debug`, `info` or `error`
- `GATEWAY_SERVICE_PORT`: port that this service will run on

Tokens:
- `ACCESS_TOKEN_TTL`: access token's time to live in seconds
- `REFRESH_TOKEN_TTL`: refresh token's time to live in seconds
- `ACCESS_TOKEN_KEY`: string that will be used as the cookie key for the access token
- `REFRESH_TOKEN_KEY`: string that will be used as the cookie key for the refresh token

Other:
- `FRONTEND_URL`: full url to the **Frontend**. Used for CORS stuff in the **Gateway service**
- `MAX_REQUEST_BODY_SIZE`: max request body size for file uploads in megabytes
- `MAX_FILE_CHUNK_SIZE`: max size for gRPC messages that transfer file chunks in megabytes
