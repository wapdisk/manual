# 下载安装

V2Ray 对于常见操作系统发布了一系列的预编译程序，直接下载即可使用，无须从源代码重新编译。预编译程序发布于 [Release](https://github.com/v2ray/v2ray-core/releases) 中，每周更新。

支持的平台如下：
* Windows: Vista 及之后版本，32 位和 64 位；
* Mac OS X: 10.7 (Lion) 及之后版本，64位；
* Linux：Kernel 2.6.23 及之后版本，如 Debian 7+， Ubuntu 12.04+，CentOS 6+ 等。

## Windows / Mac OS X
下载上述的发行包，解压即可使用。

## Linux
V2Ray 提供了一个安装脚本用于在 Linux 环境的安装和配置。这个脚本会自动检测有没有安装过 V2Ray，如果没有，则进行完整的配置；如果之前安装过 V2Ray，则只更新 V2Ray 二进制程序而不更新配置。

以下指令假设已在 su 环境下，如果不是，请先运行 sudo su。

运行下面的指令下载并安装 V2Ray。当 yum 或 apt-get 可用的情况下，此脚本会自动安装 unzip 和 daemon。这两个组件是安装 V2Ray 的必要组件。如果你使用的系统不支持 yum 或 apt-get，请自行安装 unzip 和 daemon
```bash
bash <(curl -L -s https://raw.githubusercontent.com/v2ray/v2ray-core/master/release/install-release.sh)
```
 
此脚本会自动安装以下文件：
* /usr/bin/v2ray/v2ray：V2Ray 程序；
* /etc/v2ray/config.json：配置文件；

此脚本会配置自动运行脚本。自动运行脚本会在系统重启之后，自动运行 V2Ray。目前自动运行脚本只支持带有 Systemd 的系统，以及 Debian / Ubuntu 全系列。

脚本运行完成后，你需要：

1. 编辑 /etc/v2ray/config.json 文件来配置你需要的代理方式；
1. 运行 service v2ray start 来启动 V2Ray 进程；
1. 之后可以使用 service v2ray start|stop|status|reload|restart|force-reload 控制 V2Ray 的运行。

### install-release.sh 参数
install-release.sh 支持如下参数，可在手动安装时根据实际情况调整：

* -p 或 --proxy: 使用代理服务器来下载 V2Ray 的文件，格式与 curl 接受的参数一致，比如 socks5://127.0.0.1:1080 或  http://127.0.0.1:3128。
* -f 或 --force: 强制安装。在默认情况下，如果当前系统中已有最新版本的 V2Ray，install-release.sh 会在检测之后就退出。如果需要强制重装一遍，则需要指定该参数。
* --version: 指定需要安装的版本，比如 v1.13。默认值为最新版本。
* --local: 使用一个本地文件进行安装。如果你已经下载了某个版本的 V2Ray，则可通过这个参数指定一个文件路径来进行安装。

**用例**

* 使用地址为 127.0.0.1:1080 的 SOCKS 代理下载并安装最新版本：```./install-release.sh -p socks5://127.0.0.1:1080```
* 安装本地的 v1.13 版本：```./install-release.sh --version v1.13 --local /path/to/v2ray.zip```
