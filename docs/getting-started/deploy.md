# Deploy

Deploy your service with Abel is easier than ever. It only takes an HTTP request to upload the source code to the server and ready to run.

First, make sure you have `abel server` running on the host machine, and can be accessible through HTTP:

```console
$ abel server
 INFO  abel > Starting abel-server v0.1.0
 INFO  abel > Abel working path: $HOME/.abel
 INFO  abel > Authentication token: <your-auth-token>
 INFO  abel::server > Abel is listening to 127.0.0.1:3000
```

A reverse proxy is recommended, since Abel currently does not support HTTPS server.

Then deploy your service, simply with , with header `Authorization: Abel <your-auth-token>`:

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

For server configuration, see [Manual/Server/Configuration](../server/config.md).
