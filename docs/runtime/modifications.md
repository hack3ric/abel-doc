# Modifications

Abel heavily modifies Lua environment and replaces some of the Lua's standard library with its own implementation for great isolation and concurrency. It also removes "unsafe" functions to prevent potential sandbox escaping.

Some part of the Lua standard library is removed:

- `rawget` and `rawset`: force metatable to be followed
- `string.dump`: provides access to function bytecode
- `load` and `loadfile`: access to filesystem
- `debug`: violates memory safety model
- `os`: environment access
- `package`: reimplemented and moved to internal table
- `io`: removed functions related to stdio and process

Some functions are re-implemented:

- Module imports has been redesigned. See [Imports]() for more information.
- Error handling functions (including `error`, `assert` and `pcall`) allows HTTP errors to be thrown. See [Error Handling]() for more information.
- `getmetatable` now only accepts tables as argument.
- `io.{open,tmpfile,type}` and `os.{remove,rename}` now uses Tokio-enabled asynchronous API and follows sandbox rules. See [`fs` module](../api/runtime/fs.md) for more information.
- `os.getenv`: currently always return `nil`, will return environment variables specified in config file in the future.
