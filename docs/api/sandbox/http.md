# HTTP

The HTTP module provides basic HTTP types, such as `Request`, `Response` and `Uri`, as well as a `http.request` function for easy requests. 

```lua
local http = require "http"
```

## Methods

### http.request

```ts
http.request(uri: string | Uri) -> Result<Response>
```

```ts
http.request(req: {
  method?: string = "GET",
  uri: string,
  headers?: { [key: string]: string | string[] },
  body?: Body,
}) -> Result<Response>
```

Sends an HTTP request. You can either use a single URI to send GET requests, or use other methods, add headers or a body with the latter builder table.

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

You don't need to manually create a `Request` yourself — either receive one in `abel.listen`'s handlers, or send one using a builder table in `http.request`.

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

Extracted path parameters. Only used in `abel.listen`'s handlers.

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

### Body

```ts
type Body = nil | string | Value | ByteStream
```

HTTP body representation. It could be nil, a string, a JSON value, or a `ByteStream`.

Note that the `Body` returned from methods or callbacks is always `ByteStream`. However, you can use one of the aforementioned types in custom requests and responses.

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
Uri:query() -> Result<QueryMap>
```

Parses the query string of the URI, returning a map of query.

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

### QueryMap

```ts
type QueryMap = { [key: string]: string | string[] | QueryMap | QueryMap[] }
```
