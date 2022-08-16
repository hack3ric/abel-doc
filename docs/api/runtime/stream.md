# Stream

A stream of values produced asynchronously, usually bytes (strings).

```lua
local stream = require "stream"
```

## Internal Types

Unless noted, most internal types that implements `Stream`, `Sink` or `Transform` have this module linked in its `__index` metamethod. Therefore, you should be able to do chain calls like this:

```lua
req.body
  :pipe_through(my_transform)
  :pipe_to(file)
```

instead of

```lua
stream.pipe_to(stream.pipe_through(req.body, my_transform), file)
```

## Interfaces

### Stream

```ts
interface Stream<T> {
  read: (self) -> T
}
```

### BufStream

```ts
interface BufStream extends Stream<string> {
  read: (self, mode: ReadMode) -> T
}
```

### Sink

```ts
interface Sink<T> {
  write: (self, item: T) -> nil
}
```

### Transform

```ts
interface Transform<T, U> {
  transform: (self, item: T) -> U
}
```

## Types

### ByteStream

```ts
type ByteStream: Stream<string> = <userdata>
```

Native byte stream.

### ReadMode

```ts
type ReadMode = integer | "a" | "l" | "L"
```

## Methods

### stream.read_all

```ts
stream.read_all(st: Stream<string>) -> string
```

### stream.parse_json

```ts
stream.parse_json(st: Stream<string>) -> Value
```

### stream.iter

```ts
stream.iter<T>(st: Stream<T>) -> iterator<T>
```

### stream.from_iter

```ts
stream.from_iter<T>(iter: iterator<T>) -> Stream<T>
```

### stream.pipe_to

```ts
stream.pipe_to<T>(st: Stream<T>, sink: Sink<T>)
```

### stream.pipe_through

```ts
stream.pipe_through<T, U>(st: Stream<T>, tr: Transform<T, U>) -> Stream<U>
```

### stream.recv_from

```ts
stream.recv_from<T>(sink: Sink<T>, st: Stream<T>)
```

### stream.recv_through

```ts
stream.recv_through<T, U>(sink: Sink<U>, tr: Transform<T, U>) -> Sink<T>
```
