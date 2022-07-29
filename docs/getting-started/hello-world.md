# Hello, World

The simpliest form of a Abel service is a single Lua file. So let's begin by creating a file named `hello.lua`:

```lua
-- hello.lua

local function hello(req)
  local name = req.params.name or "world"
  return {
    greeting = "Hello, " .. name .. "!"
  }
end

-- The former `listen` is to listen to the "root path", which will the default
-- name "world". The latter one matches exactly one path segment, and extracts that
-- segments into `req.params.name`.
abel.listen("/", hello)
abel.listen("/:name", hello)
```

Start your Abel server in dev mode. This creates a temporary working environment for you to play on:

```console
$ abel dev hello.lua
 INFO  abel > Starting abel-server v0.1.0 (dev mode)
 INFO  abel::server > Loaded service (89a90b6b-2555-48ef-852d-9fc930a5a5e4)
 INFO  abel::server > Abel is listening to 127.0.0.1:3000
```

Now your hello world should be ready. Access it through HTTP:

```console
$ curl 127.0.0.1:3000/hello
{"greeting":"Hello, world!"}

$ curl 127.0.0.1:3000/hello/Eric
{"greeting":"Hello, Eric!"}
```

In dev mode, Abel also watches the file for changes and hot update it. Try to modify `hello.lua`:

```lua
  return {
    greeting = "Hello, " .. name:upper() .. "!"
  }
```

Then access it again. Now your name is screamed out!

```console
$ curl 127.0.0.1:3000/hello
{"greeting":"Hello, WORLD!"}

$ curl 127.0.0.1:3000/hello/Eric
{"greeting":"Hello, ERIC!"}
```

Voila! You just finished your first Abel service!
