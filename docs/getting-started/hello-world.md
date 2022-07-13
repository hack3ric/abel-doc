# Hello, World

The simpliest form of a Abel service is a single Lua file. So let's begin by creating a file named `hello.lua`:

```lua
-- hello.lua

local function hello(req)
  local name = req.params.name or "world"
  return {
    greeting = string.format("Hello, %s", name)
  }
end

-- The former register is to listen to the "root path", which will the default
-- name "world". The latter one matches exactly one path segment, and extracts that
-- segments into `req.params.name`.
abel.register("/", hello)
abel.register("/:name", hello)
```

Start your Abel server:

```console
$ abel-server
 INFO abel_server > Authentication token: f5db97cd-2eb4-45ad-a5d9-2d4a1dd80fec
 INFO abel_server > Abel is listening to 127.0.0.1:3000
```

Upload your service to that server with the authentication token. Note that the header name is `Authorization`, not `Authentication`.

```console
$ curl -X PUT 127.0.0.1:3000/services/hello \
  -H "Authorization: Abel f5db97cd-2eb4-45ad-a5d9-2d4a1dd80fec" \
  -F single=@hello.lua \
  | jq
{
  "new_service": {
    "name": "hello",
    ...
  }
}
```

Now your hello world should be ready. Access it through HTTP, again:

```console
$ curl 127.0.0.1:3000/hello
{"greeting":"Hello, world!"}

$ curl 127.0.0.1:3000/hello/Eric
{"greeting":"Hello, Eric!"}
```

Voila! You just finished your first Abel service!
