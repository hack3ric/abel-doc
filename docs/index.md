---
hide:
  - navigation
---

# Welcome to Abel Documentation

[Abel](https://github.com/hack3ric/abel) is a lightweight microservices framework for Lua. It focuses on simple, fun experience of writing modular web services.

Abel's name comes from *abelo*, which means bee in Esperanto. It further comes from *abelujo*, which means Hive (the project's former name).

## Getting Started

There are a few places you can start reading:

- If you haven't learned Lua yet, [the official Lua 5.4 reference](https://www.lua.org/manual/5.4/) is a good way to go.
- [Manual](/getting-started/installation) contains introduction to aspects of Abel.
- [API reference](/api/builtins) contains detailed definition of Sandbox API.

## Features

- Fully multi-threaded & asynchronous
- Writing, deploying and iterating Lua microservices without breaking a sweat
- Compliant to HTTP standards and JSON RESTful API conventions
- Sandbox environment, with limited yet powerful Sandbox API

## Basic Concepts

Abel follows three major principles:

- **Asynchronous.** Reading a file, requesting an API, or other things that can be made asynchronous, will never block other instance to execute.

- **Sandboxed.** an Abel service can only access its own contained resources, and is fully blocked from the outside world.

- **Standardized.** Abel conforms with HTTP standards and RESTful JSON API conventions (unless you want to break them intentionally).

Thanks to [Rust](https://rust-lang.org), [Tokio](https://tokio.rs), [Hyper](https://hyper.rs) and [Lua](https://lua.org) (as well as its binding [mlua](https://github.com/khvzak/mlua)), these ideal designs are way easier to realize.

## Lua Version Compatibility

Abel currently uses Lua 5.4 as its runtime. Lower versions and LuaJIT support is under consideration for now.

## License

Abel is licensed under the MIT License.
