# Security

One core feature of Abel is security. Services' behaviour is contained within its own realm, and cannot access the outside world unless specified.

## Local environment

On a Lua state, each service runs on their own, isolated local environment. It forms the basis of Abel's sandboxing, and you won't notice it while writing scripts.

## Restricted API set

Abel enables a safe subset of the Lua standard library to prevent services from escaping sandbox, modifying the environment, etc.

See [Modifications](modifications.md) for a detailed list of what's changed.

```lua
-- Here are some examples of removed "unsafe" APIs.

print(rawset)  -- nil
print(os.exit) -- nil
print(debug)   -- nil
```

## Limited file system

Services are provided with a contained, `chroot`-like file system to persistently store files. Other part of the entire file system is inaccessible.

```lua
-- No way to get that file removed — the file system's completely isolated!
os.remove "/super/important/system/file"
```

## Automatic `<close>`

Lua 5.4 introduced local variable attributes `<const>` and `<close>`, the latter of which provides [RAII] functionality similar to Rust's. Abel bring this even further: files, sockets, etc. will be automatically `<close>`d after exiting a certain scope, even it isn't tagged `<close>`. This prevents resource leaking and starvation of process resources such as file handles, as well as eliminates the need of waiting GC to do the job.

```lua
abel.listen("/", function(req)
  -- Oops, forgot to add `<close>`!
  local file, err = io.open("/storage.csv", "a")
  assert(file, err)

  do_something(file)
  return { ... }
  -- Don't worry, the file will be closed at the end of the scope!
end)
```

!!! warning
    Currently custom objects that implements the metamethod `__close` is not supported this feature. This may be feasible in the future.

!!! tip
    Although Abel prevents resource leaking, adding `<close>` to those objects or freeing them after usage is always a good habit.

    ```lua
    local file <close>, err = io.open("/storage.csv", "a")
    assert(file, err)
    do_something(file)

    -- or free it manually
    local file, err = io.open("/storage.csv", "a")
    assert(file, err)
    do_something(file)
    file:close()
    ```

[RAII]: https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization
