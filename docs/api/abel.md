# Abel API

This contains APIs that is associated with Abel's executor, error handling, logic, etc.

## Methods

### abel.current_worker

```ts
abel.current_worker() -> string
```

Returns the current worker thread's name. Usually the names are `abel-worker-{i}`.

### abel.Error

```ts
abel.Error(error: {
  status?: integer,
  error?: string,
  detail?: Value,
}) -> table
```

Allows to define an error kind, and reuse it with additional details.

Returns the table `error` as is, with a metatable attached to it. It can be called as a function with an argument `detail`, returning the table with the original `status` and `error`, and the new `detail`.

#### Examples

```lua
local not_an_integer = abel.Error {
  status = 400,
  error = "not an integer"
}

abel.register("/:n", function(req)
  local n = math.tointeger(req.params.n)
  if not n then
    error(not_an_integer { got = req.params.n })
  end
end)
```

## Fields

### abel.start

```ts
abel.start?: function()
```

The service's start hook.

If it's a function, it's called every time the service starts.

### abel.stop

```ts
abel.stop?: function()
```

The service's start hook.

If it's a function, it's called every time the service stops.
