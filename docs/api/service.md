# Service API

Service API is the HTTP interface of service management.

## Authentication

Currently, Abel uses one UUID as authentication token, and is stored in `$ABEL_PATH/config.json`. To authorize yourself, you need to pass this token through `Authorization` header with the scheme `Abel`:

```console
$ curl https://abel.example.com/services \
    -H "Authorization: Abel <your-auth-token>"
```

In the future, other authentication methods may be implemented.

## Methods

### GET /services

Get all currently existing services.

### GET /services/:service

Get the detailed information of a service.

### PUT /services/:service

Uploads a service.

#### Query

- `mode`: Specifies how the services should be uploaded. Available options are:
    - `create`: (Default) creates the service, errors if service exists
    - `hot`
    - `cold`
    - `load`

#### Multipart Fields

- `single`: Specifies a single-file service (a Lua source file).
- `multi`: Specifies a multi-file service (an asar archive).

### PATCH /services/:service

#### Query

- `op`
    - `start`
    - `stop`

### DELETE /services/:service

Deletes the service.
