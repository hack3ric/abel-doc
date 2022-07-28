# Abel API

This contains APIs that is associated with Abel's executor, error handling, logic, etc.

## Methods

### abel.listen

```ts
abel.listen(path: string, handler: (req: Request) -> Response | Body)
```

Registers a path and listens to it.

The path matches in `listen`'s calling order: first handler `listen`ed is first matched. For example:

```lua
-- '/foo/bar' will go to `handler1`, while '/foo/baz' will go to `handler2`.
abel.listen("/foo/bar", handler1)
abel.listen("/foo/:value", handler2)

-- However, if you switch the order of the two statements, even '/foo/bar' will be
-- matched into `handler2` because '/foo/:value' matches first.
abel.listen("/foo/:value", handler2)
abel.listen("/foo/bar", handler1)
```

### abel.current_worker

```ts
abel.current_worker() -> string
```

Returns the current worker thread's name. Usually the names are `abel-worker-{i}`.

### abel.spawn

```ts
abel.spawn<T>(fn: (...args: any) -> T, ...args: any) -> Promise<T>
```

Spawns a new task that runs on the same thread concurrently with the current one. It shares the same context with the task calling `spawn`.

Returns a [Promise](builtins.md#promise) that can be `await`ed at any time.

### abel.sleep

```ts
abel.sleep(ms: integer)
```

Pauses the currently running tasks for *at least* a certain period of time `ms` in milliseconds, letting other tasks on the same executor to run. It does not account for CPU time.

When `ms` is set to zero, it has the same effect as `coroutine.yield()`, which simply hands over the control of the executor to other tasks.

Fails if `ms` is negative.

## Fields

### abel.start

```ts
abel.start?: () -> any
```

The service's start hook.

If it's a function, it's called every time the service starts.

### abel.stop

```ts
abel.stop?: () -> any
```

The service's start hook.

If it's a function, it's called every time the service stops.
