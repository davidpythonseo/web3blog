---
title: "Web3"
date: 2023-06-13T23:27:04+08:00
draft: false
ShowToc: true
TocOpen: true
---

# Web3 community

## AdsPower API

- AWS cloud + email + us fake KYC
- https://aws.amazon.com/
- Amazon Lightsail
- https://blog.51cto.com/pure/5566924
- how to create socks5 proxy server
- 结合 AdsPower API + Python selenium


- 下载脚本
```bash
wget —no-check-certificate https://raw.github.com/Lozy/danted/master/install.sh -O install.sh
```
---
- 脚本代码
```bash
#!/bin/bash
#
#   Dante Socks5 Server AutoInstall
#   -- Owner:       https://www.inet.no/dante
#   -- Provider:    https://sockd.info
#   -- Author:      Lozy
#

# Check if user is root
if [ $(id -u) != "0" ]; then
    echo "Error: You must be root to run this script, please use root to install"
    exit 1
fi

REQUEST_SERVER="https://raw.github.com/Lozy/danted/master"
SCRIPT_SERVER="https://public.sockd.info"
SYSTEM_RECOGNIZE=""

[ "$1" == "--no-github" ] && REQUEST_SERVER=${SCRIPT_SERVER}

if [ -s "/etc/os-release" ];then
    os_name=$(sed -n 's/PRETTY_NAME="\(.*\)"/\1/p' /etc/os-release)

    if [ -n "$(echo ${os_name} | grep -Ei 'Debian|Ubuntu' )" ];then
        printf "Current OS: %s\n" "${os_name}"
        SYSTEM_RECOGNIZE="debian"

    elif [ -n "$(echo ${os_name} | grep -Ei 'CentOS')" ];then
        printf "Current OS: %s\n" "${os_name}"
        SYSTEM_RECOGNIZE="centos"
    else
        printf "Current OS: %s is not support.\n" "${os_name}"
    fi
elif [ -s "/etc/issue" ];then
    if [ -n "$(grep -Ei 'CentOS' /etc/issue)" ];then
        printf "Current OS: %s\n" "$(grep -Ei 'CentOS' /etc/issue)"
        SYSTEM_RECOGNIZE="centos"
    else
        printf "+++++++++++++++++++++++\n"
        cat /etc/issue
        printf "+++++++++++++++++++++++\n"
        printf "[Error] Current OS: is not available to support.\n"
    fi
else
    printf "[Error] (/etc/os-release) OR (/etc/issue) not exist!\n"
    printf "[Error] Current OS: is not available to support.\n"
fi

if [ -n "$SYSTEM_RECOGNIZE" ];then
    wget -qO- --no-check-certificate ${REQUEST_SERVER}/install_${SYSTEM_RECOGNIZE}.sh | \
        bash -s -- $*  | tee /tmp/danted_install.log
else
    printf "[Error] Installing terminated"
    exit 1
fi

exit 0
```
- 安装脚本赋权限 执行安装脚本 配置端口 用户信息

```bash
chmod +x install.sh && ./install.sh --port=7788 --user=david --passwd=pythonseo
```
- sockd 使用菜单
```bash
Usage: /etc/init.d/sockd {start|stop|restart|reload|status|state|adduser|deluser|tail|conf|update}
```
- 防火墙放行端口

```bash
firewall-cmd --add-port=1000-60000/udp --permanent
```


## MetaMask 小号

- 钱包的安全使用密钥保管

## Discord 小号 + community

## Twitter 小号 + 媒体号

## Github 小号 + 域名

## Gitcoin 

## 