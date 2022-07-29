# Testing

Testing utilities.

```lua
local testing = require "testing"
```

## Methods

### testing.assert

```ts
testing.assert<T>(value: T, msg?: any) -> T
```

*Re-exported from `assert`*

Throws error if `value` *is not* a truthy value (all values except `false` and `nil`), otherwise return it as is.

### testing.assert_false

```ts
testing.assert_false(value: any, msg?: any)
```

Throws error if `value` *is* a truthy value (all values except `false` and `nil`).

### testing.assert_eq

```ts
testing.assert_eq<T>(left: T, right: T, msg?: any)
```

Throws error if `left` and `right` *are not* equal.

### testing.assert_ne

```ts
testing.assert_ne<T>(left: T, right: T, msg?: any)
```

Throws error if `left` and `right` *are* equal.
