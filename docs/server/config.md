# Configuration

Abel's server configuration files is located in `$ABEL_DIR/config.json`, where `$ABEL_DIR` defaults to `~/.abel`.

A default configuration files looks like this:

```json
{
  "listen": "127.0.0.1:3000",
  "auth_token": "<random-auth-token>",
  "pool_size": null
}
```

The configurable options are:

- `listen`: The address Abel server will be listening to.
- `auth_token`: Authentication token. This can be set to `null` to remove authentication, but don't do this in production environment!
- `pool_size`: Lua executor count. Defaults to <code><a href="https://doc.rust-lang.org/std/thread/fn.available_parallelism.html">std::thread::available_parallelism()</a> / 2</code> if the value is set to `null`.

These options are overridable with command line options, but the `config.json` will remain the same:

```console
$ abel-server --listen 0.0.0.0:1024 --auth-token <new-auth-token>
 INFO abel_server > Authentication token: <new-auth-token>
 INFO abel_server > Abel is listening to 0.0.0.0:1024
```
