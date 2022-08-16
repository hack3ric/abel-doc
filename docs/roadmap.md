# Roadmap

This is a (incomplete) list of upcoming features. Some of them have a tracking issue attached.

## Lua API

- Remote `require` [#7](https://github.com/hack3ric/abel/issues/7)
- `multipart/form-data` support
- Static file serving
- Cron triggers
    - Can be hashed (a.k.a. scheduling jitter), like the one used in Jenkins
- Function calls between services
- Workers (similar to Web Worker)

## User Experience

- Custom sandbox parameters (e.g. CPU timeout)
- Clients and dev utilities in `abel` CLI
    - Wraps the REST API, while providing more such as packaging, custom script, pre- and post-deploy actions, and much more
    - Like npm without pm (the package manager part is in remote `require` above)
- Hosting repository like [deno.land/x](https://deno.land/x)

## Security

- HTTPS server
