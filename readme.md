# RealM
> A network relay tool

## Introduction

realm is a simple, high performance relay server written in rust.

## Features
- Zero configuration. Setup and run in one command.
- Concurrency. Bidirectional concurrent traffic leads to high performance.
- Low resources cost.

## Custom Build
Available Options:
- udp *(enabled)*
- tfo *(enabled)*
- zero-copy *(enabled on linux)*

```shell
# simple tcp
cargo build --release --no-default-features

# enable other options
cargo build --release --no-default-features --features udp, tfo, zero-copy
```

## 安装脚本
> 脚本根据 seal0207 版修改

国外
```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/xOS/RealM/master/realm.sh && chmod +x realm.sh && ./realm.sh
```

国内
```bash
wget -N --no-check-certificate https://cdn.jsdelivr.net/gh/xOS/RealM@master/realm.sh && chmod +x realm.sh && ./realm.sh
```

## Usage
```shell
Realm 1.x
A high efficiency proxy tool

USAGE:
    realm [FLAGS] [OPTIONS] [SUBCOMMAND]

FLAGS:
    -h, --help       Prints help information
    -u, --udp        enable udp
    -V, --version    Prints version information

OPTIONS:
    -c, --config <path>    use config file
    -l, --listen <addr>    listen address
    -r, --remote <addr>    remote address
```

Start from command line arguments:
```shell
realm -l 127.0.0.1:5000 -r 1.1.1.1:443 --udp
```

Use a config file:
```shell
realm -c config.json
```
```json
{
	"dns_mode": "ipv4_only",
	"endpoints": [
		{
			"local": "0.0.0.0:5000",
			"remote": "1.1.1.1:443",
			"udp": false
		},
        {
			"local": "0.0.0.0:10000",
			"remote": "www.google.com:443",
			"udp": true
		}
	]
}
```
dns_mode:
- ipv4_only
- ipv6_only
- ipv4_then_ipv6 *(default)*
- ipv6_then_ipv4
- ipv4_and_ipv6
