# JSON

```lua
local json = require "json"
```

## Methods

### json.parse

```ts
json.parse(str: string) -> Value
```

Parses the JSON string to value.

### json.stringify

```ts
json.stringify(value: Value, pretty?: boolean) -> string
```

### json.array

```ts
json.array(t: table) -> table
```

### json.undo_array

```ts
json.undo_array(t: table) -> table
```

## Types

### Value

```ts
type Value = nil | boolean | number | string | Value[] | { [key: string]: Value }
```

Valid JSON value. It could be one of nil (no such field or null), boolean, number, string, string-keyed table or array.

Note that tables with recursion is invalid JSON value. Attempt to use them on `json.stringify` will result in an error.

## Fields

### json.array_metatable

```ts
json.array_metatable: table
```
