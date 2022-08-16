# Deploy

## Deploy Abel

Simply run `abel server` to start the server:

```console
$ abel server
 INFO  abel > Starting abel-server v0.1.0
 INFO  abel > Abel working path: $HOME/.abel
 INFO  abel > Authentication token: <your-auth-token>
 INFO  abel::server > Abel is listening to 127.0.0.1:3000
```

For server configuration, see [Manual/Server/Configuration](../server/config.md).

## Deploy Services

Deploy your service with Abel is easier than ever. It only takes an HTTP request to upload the source code to the server and ready to run.

### via CLI

```console
$ abel deploy path/to/service \
  --server https://abel.example.com \
  --auth-token <your-auth-token>
```

or use environment variables to specify them. This can be used along with tools like dotenv for your convenience.

```console
$ export ABEL_SERVER=https://abel.example.com
$ export ABEL_AUTH_TOKEN=<your-auth-token>
$ abel deploy path/to/service
```

### via HTTP

Deploy your service using an HTTP client (here uses curl as example), with header `Authorization: Abel <your-auth-token>`:

```console
$ curl https://abel.example.com/services/awesome-service \
  -X PUT \
  -H "Authorization: Abel <your-auth-token>" \
  -F multi=@... | jq
{
  "new_service": {
    "name": "awesome-service",
    // ...
  }
}
```

Now anyone can easily run it through HTTP. Easy, isn't it?

```console
$ curl https://abel.example.com/awesome-service
```

For more methods to manage the service on the fly, see [API/Server/Service](../api/server/service.md).
