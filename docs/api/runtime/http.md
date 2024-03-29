# HTTP

The HTTP module provides basic HTTP types, such as `Request`, `Response` and `Uri`, as well as a `http.request` function for easy requests. 

```lua
local http = require "http"
```

## Methods

### http.request

```ts
http.request(uri: string | Uri) -> Response
```

```ts
http.request(req: {
  method?: string = "GET",
  uri: string,
  headers?: { [key: string]: string | string[] },
  body?: Body,
}) -> Response
```

Sends an HTTP request. You can either use a single URI to send GET requests, or use other methods, add headers or a body with the latter builder table.

For convenience, any underscore (`_`) in `headers`' keys is replaced with dash (`-`). To avoid that, use `@` prefix:

```lua
http.request {
  headers = {
    x_my_custom_header = "foo bar" -- sends `x-my-custom-header`
  }
}

http.request {
  headers = {
    ["@x_my_custom_header"] = "foo bar" -- sends "x_my_custom_header"
  }
}
```

#### Examples

The simpliest usage is to send a GET request to the server using a single URI:

```lua
local http = require "http"

local resp, err = http.request "https://httpbin.org/get"
assert(resp, err)
```

Send an HTTP POST request with body and `User-Agent` header:

```lua
local http = require "http"

local resp, err = http.request {
  method = "POST",
  uri = "https://httpbin.org/post",
  body = "Hello, world!",
  headers = {
    ["user-agent"] = "abel/0.1.0"
  }
}
assert(resp, err)
```

## Types

### Request

```ts
type Request = <userdata>
```

HTTP request representation.

You don't need to manually create a `Request` yourself — either receive one in [`abel.listen`](abel.md#abellisten)'s handlers, or send one using a builder table in `http.request`.

#### Request.method

```ts
Request.method: string
```

The request's method.

#### Request.uri

```ts
Request.uri: Uri
```

The request's URI, parsed into `Uri` userdata.

#### Request.headers

```ts
Request.headers: HeaderMap
```

The request's header map.

#### Request.body

```ts
Request.body: Body
```

The request's body.

#### Request.params

```ts
Request.params: { [key: string]: string }
```

Extracted path parameters. Only used in [`abel.listen`](abel.md#abellisten)'s handlers.

### Response

```ts
type Response = <userdata>
```

HTTP response representation.

#### http.Response

```ts
http.Response(builder: {
  status?: integer = 200,
  headers?: { [key: string]: string | string[] },
  body?: Body
}) -> Response
```

#### Response.status

```ts
Response.status: integer
```

#### Response.header

```ts
Response.header: HeaderMap
```

#### Response.body

```ts
Response.body: Body
```

### Body

```ts
type Body = nil | string | Value | Stream<string>
```

HTTP body representation. It could be nil, a string, a JSON value, or a stream of strings.

Note that the `Body` returned from methods or callbacks is always [`ByteStream`](stream.md#bytestream). However, you can use one of the aforementioned types in custom requests and responses.

### Uri

```ts
type Uri = <userdata>
```

Parsed URI, either absolute or relative.

#### http.Uri

```ts
http.Uri(uri: string) -> Uri
```

```ts
http.Uri(builder: {
  scheme?: string,
  authority?: string,
  path_and_query?: string,
  path?: string,
  query?: QueryMap
}) -> Uri
```

Parses a URI from string, or build one using a builder table.

Fragments in URIs are ignored, since these are not sent to the server in normal cases.

#### Uri:query

```ts
Uri:query() -> QueryMap
```

Parses the query string of the URI, returning a map of query as [`QueryMap`](#querymap).

Returns error if parsing query string failed.

##### Examples

```lua
local http = require "http"

local uri = http.Uri "https://example.com/?foo=bar&baz=hello%20world"
local query, err = uri:query()
assert(query, err)

-- Note that URI escapes are resolved (in this case the space `%20`)
assert(query.foo == "bar")
assert(query.baz == "hello world")
```

#### Uri.scheme

```ts
Uri.scheme: string
```

#### Uri.host

```ts
Uri.host: string
```

#### Uri.port

```ts
Uri.port: integer
```

#### Uri.authority

```ts
Uri.authority: string
```

#### Uri.path

```ts
Uri.path: string
```

#### Uri.query_string

```ts
Uri.query_string: string
```

### HeaderMap

```ts
type HeaderMap = <userdata>
```

Map of HTTP headers.

Can be indexed or iterated using `pairs`.

```lua
print("The content type is: " .. req.headers.content_type)

print "Full header list:"
for k, v in pairs(req.headers) do
  print(k .. ": " .. v)
end
```

When indexed, underscores (`_`) can be used as dashes (`-`), as the above code shows. If you do want to access a field with underscores in its name, you can use `@` prefix: 

```lua
local my_header = req.headers["@header_with_underscore"]
```

#### HeaderMap:get

```ts
HeaderMap:get(key: string) -> ...string
```

Get one or more header field of the name `key`.

This method strictly matches its name, meaning that it does not replace underscores in `key` or use `@` prefix.

### QueryMap

```ts
type QueryMap = { [key: string]: string | string[] | QueryMap | QueryMap[] }
```

Representing an URI's query structure, with multi-level support.
