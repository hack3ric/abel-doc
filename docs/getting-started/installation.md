# Installation

Abel is tested to work on macOS, Linux and Windows on the x86-64 architecture. Other architectures may also work, it's just not tested.

Currently, Abel is still under heavy development, and is not published in repositories. So if you want to give it a try, you'll have to clone and compile it yourself.

## Manual

### Prerequisites

- Lastest stable version of Rust (upon Abel's version release)
- GCC or GCC-compatible C compilers (for compiling Lua)
- make (for compiling Lua)
- (On Linux) OpenSSL or LibreSSL development libraries (for example, `libssl-dev` on Debian and Ubuntu)

### Clone and Compile

```console
$ git clone https://github.com/hack3ric/abel
$ cd abel
$ cargo install --path abel-server
```

And that's it! Your Abel is ready.
