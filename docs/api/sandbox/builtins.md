# Builtins

## Methods

### HttpError

```ts
HttpError(error: {
  status?: integer,
  error?: string,
  detail?: Value,
}) -> table
```

Allows to define an error kind, and reuse it with additional details.

Returns the table `error` as is, with a metatable attached to it. It can be called as a function with an argument `detail`, returning the table with the original `status` and `error`, and the new `detail`.

#### Examples

```lua
-- Service 'int-echo'

local not_an_integer = HttpError {
  status = 400,
  error = "not an integer"
}

abel.listen("/:n", function(req)
  local n = math.tointeger(req.params.n)
  if not n then
    error(not_an_integer { got = req.params.n })
  end
  return { int = n }
end)
```

```console
$ curl abel.example.com/int-echo/5 -v | jq
< HTTP/1.1 200 OK
{
  "int": 5
}
$ curl abel.example.com/int-echo/3.14 -v | jq
< HTTP/1.1 400 Bad Request
{
  "error": "not an integer",
  "got": "3.14"
}
```

### debug_fmt

```ts
debug_fmt(value: any) -> string
```

Formats the value into string in Rust debug style.

## Types

### Result

```ts
type Result<T> = T | (nil, string)
```

Indicates a fallible result. On success, it outputs the value typed `T` as usual (maybe multiple values); on error, the first return value is `nil`, followed by a string describing the error.

It is still possible for a function that returns `Result<T>` to throw basic usage errors, and this type is only meant to handle user inputs, file system, networking, etc. that a developer can't control.

!!! tip

    If you want to throw the error anyway, an `assert` will handle it with ease:

    ```lua
    local fs = require "fs"

    local file <close>, err = fs.open "/path/to/some/file"
    assert(file, err)

    -- Or wrap `assert` around the function
    -- But this won't work if it has more than one value returned
    local file <close>, err = assert(fs.open "/path/to/some/file")
    ```

### ByteStream

```ts
type ByteStream = <userdata>
```

A generic byte stream.

#### ByteStream:to_string

```ts
ByteStream:to_string() -> Result<string>
```

#### ByteStream:parse_json

```ts
ByteStream:parse_json() -> Result<Value>
```

### Promise

```ts
type Promise<T> = <userdata>
```

#### Promise:await

```ts
Promise<T>:await() -> T
```
