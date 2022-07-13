# File System

Provides access to a service's isolated file system. It contains several functions that are re-exported to `io` and `os` Lua standard library for compatibility.

```lua
local fs = require "fs"
```

## Methods

### fs.open

```ts
fs.open(path: string, mode: "r" | "w" | "a" | "r+" | "w+" | "a+") -> Result<File>
```

*Re-exports to `io.open`*

### fs.type

```ts
fs.type(file: any) -> nil | "file" | "closed file"
```

*Re-exports to `io.type`*

### fs.mkdir

```ts
fs.mkdir(path: string, all?: boolean) -> Result<boolean>
```

### fs.rename

```ts
fs.rename(from: string, to: string) -> Result<boolean>
```

*Re-exports to `os.rename`*

### fs.remove

```ts
fs.remove(path: string, all?: boolean) -> Result<boolean>
```

Removes a file or directory.

Compared to `os.remove`, this method adds an additional `all` flag. If enabled, it will remove the entire directory similar to `rm -r`, instead of only removing empty ones. This could be dangerous, and you should use it with great caution!

### fs.metadata

```ts
fs.metadata(path: string) -> Result<{ kind: "dir" | "file", size?: integer }>
```

## Types

### File

```ts
type File = <userdata>
```

#### File:read

```ts
File:read(...modes: ReadMode) -> Result<...string>
```

#### File:write

```ts
File:write(...str: string) -> Result<File>
```

#### File:seek

```ts
File:seek(whence: "set" | "cur" | "end", pos: integer) -> Result<integer>
```

#### File:lines

```ts
File:lines(mode: ReadMode) -> iterator<string>
```

#### File:flush

```ts
File:flush() -> Result<boolean>
```

#### File:into_stream

```ts
File:into_stream() -> ByteStream
```

### ReadMode

```ts
type ReadMode = integer | "a" | "l" | "L"
```
