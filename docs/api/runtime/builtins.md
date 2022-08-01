# Builtins

## Methods

### HttpError

```ts
HttpError(error: {
  status?: integer,
  error?: string,
  detail?: Value | (...args: any) -> Value,
}) -> table
```

Defines an custom HTTP error kind, allowing reuse with additional details.

#### Examples

```lua
-- Service 'int-echo'

local NotAnInteger = HttpError {
  status = 400,
  error = "not an integer",
  detail = function(got)
    return { got = got }
  end
}

abel.listen("/:n", function(req)
  local n = math.tointeger(req.params.n)
  if not n then
    error(NotAnInteger(req.params.n))
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

### bind

```ts
bind<T>(fn: (...args: any) -> T, ...some: any) -> (...other: any) -> T
```

## Types

### Promise

```ts
type Promise<T> = <userdata>
```

A "future value", similar to those in JavaScript.

#### Promise:await

```ts
Promise<T>:await() -> T
```

Waits for the value to resolve.

This method also propagates error when resolving the value. Note that error is *not* propagated if `await` is not called.
