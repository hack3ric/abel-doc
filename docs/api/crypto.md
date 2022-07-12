# Crypto

```lua
local crypto = require "crypto"
```

## Types

### Rng

```ts
type Rng = <userdata>
```

#### Rng:random

```ts
Rng:random() -> number
```

#### Rng:gen_range

```ts
Rng:gen_range(low: integer, high: integer) -> integer
```

## Fields

### crypto.thread_rng

```ts
crypto.thread_rng: Rng
```
