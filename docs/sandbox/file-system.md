# File System

A service have its own "local storages" - a folder where it has full control to read, write, rename and remove files. Abel re-implemented Lua's file APIs (for example, `io.open`) to provide access to the local storage in a `chroot`-like manner.

```lua
local text = "I am going to be thrown into a file!"

-- Note that path - it's in the root directory!
-- It's the same to use `foo.txt` - a slash is automatically added to the front.
local file, err = io.open("/foo.txt", "w")
assert(file, err)
file:write(text)
file:close()

os.rename("/foo.txt", "/bar.txt")

local file, err = io.open "/bar.txt"
assert(file, err)
assert(file:read "a", text)
```

## Path

There is no relative path in this environment — all paths are considered absolute. Path components like `.` and `..` are resolved.

Only UTF-8 encoded path is acceptable. Using non-UTF-8 paths will result in errors.

```lua
-- The following paths are identical:
io.open "/foo/bar/baaz.txt"
io.open "foo/bar/baaz.txt"
io.open "/foo/im/../crazy/.././bar//baaz.txt"

-- Paths with UTF-8 characters are OK!
io.open "/图片/😊.png"

-- Invalid UTF-8 path, will throw an error
io.open "/\x80\x81/test.txt"
```

## Accessing Source

Service's own source files can be accessed through URI scheme `source`.

The open mode in `io.open` is ignored; the file will always open as read-only.

```lua
local json = require "json"

local file <close>, err = io.open "source:/resources/data.json"
local data = json.parse(file:read "a")

-- Continue working on `data`...
```

!!! note
    In a single-file service, the only file — the script itself — is located in `source:/main.lua`, the same as the multi-file service's entry.

## The `fs` module

Apart from re-implemented functions in `io` and `os`, an all-in-one `fs` module is also available, containing all file system functions in standard libraries, as well as more utilities such as `mkdir` and `metadata`.

```lua
local fs = require "fs"

fs.metadata "source:/main.lua" -- { kind = "file", size = ... }
fs.metadata "/"                -- { kind = "dir" }
fs.mkdir("/foo/bar/baaz", true)
```
