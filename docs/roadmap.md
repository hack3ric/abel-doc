# Roadmap

This is a (incomplete) list of upcoming features. Some of them have a tracking issue attached.

## Lua API

- Remote `require` [#7](https://github.com/hack3ric/abel/issues/7)
- Stream API [#8](https://github.com/hack3ric/abel/issues/8)
- Key-value storage
- Workers (similar to Web Worker)

## User Experience

- Clients and dev utilities in `abel` CLI
    - Wraps the REST API, while providing more such as packaging, custom script, pre- and post-deploy actions, and much more
    - Like npm without pm (the package manager part is in remote `require`)
- Hosting repository like [deno.land/x](https://deno.land/x)

## Security

- Better authentication (instead of current one simple token)
- HTTPS server
