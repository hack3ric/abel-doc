# Modifications

Abel heavily modifies Lua environment and replaces some of the Lua's standard library with its own implementation for great isolation and concurrency. It also removes "unsafe" functions to prevent potential sandbox escaping.

Some part of the Lua standard library is removed:

- `rawget` and `rawset`: force metatable to be followed
- `string.dump`: provides access to function bytecode
- `load` and `loadfile`: access to filesystem
- `debug`: violates memory safety model
- `os`: environment and file system access
- `package`: reimplemented and moved to internal table
- `io`: stdio, process and file system access

Some functions are re-implemented:

- Module imports has been redesigned. See [Imports]() for more information.
- Error handling functions (including `error`, `assert` and `pcall`) allows HTTP errors to be thrown. See [Error Handling](error-handling.md) for more information.
- `getmetatable` now only accepts tables as argument.
- `os.getenv`: currently always return `nil`, will return environment variables specified in config file in the future.

For file system-related functions in `io` and `os`, you can use those in [`fs` module](../api/runtime/fs.md) instead. Note that APIs in `fs` differs from those counterparts.
