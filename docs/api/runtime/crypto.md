# Crypto

Cryptographic utilities.

```lua
local crypto = require "crypto"
```

## Types

### Rng

```ts
type Rng = <userdata>
```

A random number generator.

#### Rng:random

```ts
Rng:random() -> number
```

Generates a random number from the range of `[0, 1)`.

#### Rng:gen_range

```ts
Rng:gen_range(low: integer, high: integer) -> integer
```

Generates a random integer between `low` and `high`.

## Fields

### crypto.ThreadRng

```ts
crypto.ThreadRng: Rng
```

Thread-local random number generator.

Internally uses [`rand::rngs::ThreadRng`](https://docs.rs/rand/0.8.5/rand/rngs/struct.ThreadRng.html) and provides cryptographically secure randomness.
