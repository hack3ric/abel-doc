# Installation

Abel is tested to work on macOS, Linux and Windows on the x86-64 architecture. Other architectures may also work, it's just not tested.

To try out Abel, use a prebuilt binary from [Releases](https://github.com/hack3ric/abel/releases), or artifacts produced by [GitHub Actions](https://github.com/hack3ric/abel/actions/workflows/rust.yml) after every push. If there is no binary for your platform, or you want to contribute to Abel, you can also compile it yourself.

## Compile

You need:

- Lastest stable version of Rust (upon Abel's version release)
- GCC or GCC-compatible C compilers (for compiling Lua)
- make (for compiling Lua)
- (On Linux) OpenSSL or LibreSSL development libraries (for example, `libssl-dev` on Debian and Ubuntu). Not necessary if using `abel-core/tls-vendored` feature flag.
- Lua 5.4, if `abel-core/mlua-vendored` flag is disabled.

Clone and compile the project:

```console
$ git clone https://github.com/hack3ric/abel
$ cd abel
$ cargo install --path cli
```

## Install from Cargo

Install the version published in [crates.io](https://crates.io/crates/abel):

```console
$ cargo install abel --locked
```
