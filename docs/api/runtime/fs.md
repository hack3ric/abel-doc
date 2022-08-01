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

### fs.type

```ts
fs.type(file: any) -> nil | "file" | "closed file"
```

### fs.mkdir

```ts
fs.mkdir(path: string, all?: boolean)
```

### fs.rename

```ts
fs.rename(from: string, to: string)
```

*Re-exports to `os.rename`*

### fs.remove

```ts
fs.remove(path: string, all?: boolean)
```

Removes a file or directory.

### fs.metadata

```ts
fs.metadata(path: string) -> { kind: "dir" | "file", size?: integer }
```

## Types

### File

```ts
type File: Stream<string>, BufStream, Sink<string> = <userdata>
```

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

#### File:into_stream

```ts
File:into_stream() -> ByteStream
```
