# Builtins

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
ByteStream:to_string()
```
