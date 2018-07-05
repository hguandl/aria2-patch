# aria2-patch

## Introduction
Some patches to aria2. Remove connection limit and fix building on macOS.

- Enable resuming to download by default
- Set default concurrent downloads to 128
- Set default max connections to per server to 64 and remove the limit of 16 before
- Set default minimum split size to 1M
- Set default timeout to 30s
- Change the minimum unit of piece length to 1K
- Set default retry times to 2
- Set default split pieces to 128
- Disable checking certificates by default
- Fix defination of `std::make_unique` to build on maxOS.

## Usage
### Get the source code

You can download from [releases](https://github.com/aria2/aria2/releases) or [git](https://github.com/aria2/aria2).

```bash
$ git clone https://github.com/aria2/aria2.git
```

### Apply the patches from this repo

```bash
$ git clone https://github.com/hguandl/aria2-patch.git
$ cd aria2
$ patch -p1 < ../aria2-patch/aria2-fast.patch
```

### Build

For Linux users, just see [How to build](https://github.com/aria2/aria2#how-to-build).

For macOS users, please follow these steps:

1. Install dependencies from [Homebrew](https://brew.sh). To use `gettext` binary, you also need to add it to `$PATH`.
```bash
$ brew install autoconf automake libtool gettext pkg-config
$ export PATH="/usr/local/opt/gettext/bin:$PATH"
```
2. Configure and build
```bash
$ autoreconf -i
$ ARIA2_STATIC=yes CXXFLAGS="-std=c++14" ./configure --prefix=/usr/local
$ make install
```

## References
- https://www.52pojie.cn/thread-602534-1-1.html