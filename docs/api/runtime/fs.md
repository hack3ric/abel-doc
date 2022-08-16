# File System

Provides access to a service's isolated file system.

```lua
local fs = require "fs"
```

## Methods

### fs.open

```ts
fs.open(path: string, mode: "r" | "w" | "a" | "r+" | "w+" | "a+") -> File
```

Opens the file.

### fs.type

```ts
fs.type(file: any) -> nil | "file" | "closed file"
```

Check if `file` is a file instance. Returns `"file"` if it is an open file, `"closed file"` if it is a closed one, or `nil` if it is not one.

### fs.mkdir

```ts
fs.mkdir(path: string, all?: boolean)
```

Creates a directory.

Errors if `path` points to source.

### fs.rename

```ts
fs.rename(from: string, to: string)
```

Renames an entry.

Errors if `path` points to source.

### fs.remove

```ts
fs.remove(path: string, all?: boolean)
```

Removes a file or directory.

if `all` is set to true and `path` points to a directory that is not empty, it will remove all files inside it. Be careful!

Errors if `path` points to source.

### fs.metadata

```ts
fs.metadata(path: string) -> { kind: "dir" | "file", size?: integer }
```

Gets basic information about an entry.

## Types

### File

```ts
type File: Stream<string>, BufStream, Sink<string> = <userdata>
```

Representation of a file.

#### File:read

```ts
File:read(...modes: ReadMode) -> ...string
```

Reads some bytes from the file.

When no arguments is passed, a random amount of bytes is returned, which is different from files from vanilla Lua and corresponds to `Stream<string>:read`.

This method extends `BufStream:read` so that multiple read modes can be passed at the same time, returning multiple strings.

#### File:write

```ts
File:write(...bytes: string) -> File
```

Writes some bytes from the file.

This method extends `Sink<string>:write`, allowing multiple `bytes` to be written once.

#### File:seek

```ts
File:seek(whence: "set" | "cur" | "end", pos: integer) -> integer
```

#### File:lines

```ts
File:lines(mode: stream.ReadMode) -> iterator<string>
```

#### File:flush

```ts
File:flush()
```

#### File:close

```ts
File:close()
```
