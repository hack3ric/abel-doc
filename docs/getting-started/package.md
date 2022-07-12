# Package

Usually a service is more than a single `hello.lua` and consists of several source files and resources. Abel uses [asar](https://github.com/electron/asar) (the same format used in [Electron](https://github.com/electron/electron)) to pack these files.

The entry point of a package is `main.lua`. Abel will first load and execute `main.lua`, and then load other files according to usage.

## Start Packing

You can install asar according to its [installation guide](https://github.com/electron/asar#install) for now. In the future, Abel will include an asar packer by default.

Assume that you have written a service like this:
```
my-awesome-service/
  resources/
    config.json
  main.lua
  foo.lua
```

Pack those files using `asar`:
```sh
asar pack my-awesome-service my-awesome-service.asar
```

The output asar file can be deployed by using field `multi`:
```sh
curl -X PUT \
  https://abel.example.com/services/my-awesome-service \
  -F multi=@my-awesome-service.asar
```
