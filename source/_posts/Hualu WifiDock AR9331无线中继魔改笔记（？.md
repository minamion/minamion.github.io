---
title: Hualu WifiDock AR9331无线中继魔改笔记（？
date: 2019-06-20 23:31:47
tags: [Linux开发,Openwrt,硬件]
categories: [硬件,学习,Linux]
---


> 已编译完成的bin文件可从[此处](https://github.com/minamion/openwrt/releases/tag/v18.06.3-1)下载

> 懒得修改型号了 切记不要刷给wr703n 这是8m flash版本

<!-- more -->

## 关于设备：
-----------------------

AR9331的CPU 8M flash 64M DDR 自带LS 4100mah电池 20块捡回来的库存垃圾 可插TF卡和U盘 天线采用IPX接口连接（可以更换）

[![拆机图](https://i.loli.net/2019/06/20/5d0b755fc2efb26699.jpg)](https://i.loli.net/2019/06/20/5d0b755fc2efb26699.jpg)

## 刷入系统：
-----------------------

很明显官方的残废系统并不能满足我们的需求

### 刷入breed

这款无线中继硬件和TP-Link TL-WR703N非常相似 不同之处在于 复位键是在GPIO 12上 flash有8M

[![breed](https://i.loli.net/2019/06/20/5d0b7531ed82135864.png)](https://i.loli.net/2019/06/20/5d0b7531ed82135864.png)  
具体步骤：

*   开机，连接Hualu开头的WiFi。（WiFi密码12345678）
*   ping 10.10.1.1能通后，浏览器打开[http://10.10.1.1/](http://10.10.1.1/)
*   开免密Telnet 无线存储—目录名称框内输入: %24(killall telnetd;telnetd -l /bin/ash) 然后点击创建按钮（很明显这里有个注入漏洞）
*   telnet登录10.10.1.1（无需密码）。
*   电脑开hfs web服务，共享[breed文件](URL "https://breed.hackpascal.net/EOL/breed-ar9331-pisen-r1163.bin")，刷入breed
*   *   下载breed（网页上载也可以，网页上载之后，是在/tmp/usb/sda目录下）  
        ```shell
        cd /tmp/
        wget [http://10.10.1.2/breed-ar9331-pisen-r1163.bin](http://10.10.1.2/breed-ar9331-pisen-r1163.bin)
        ```
*   *   烧写  
        ```shell
        cd /tmp/
        mtd erase u-boot; mtd write breed-ar9331-pisen–GPIO12.bin u-boot 2>ubootwrite.txt
        ```
*   重启使用BreedEnter进breed
*   *   [BreedEnter](URL "https://breed.hackpascal.net/BreedEnter.zip")（需要[NpCap](URL "https://nmap.org/npcap/#download ")的winpcap兼容模式支持）

### 刷入Openwrt

[![breed](https://i.loli.net/2019/06/20/5d0b7530f1d3384567.png)](https://i.loli.net/2019/06/20/5d0b7530f1d3384567.png)  
由于硬件与WR703N基本一致 首先尝试刷入Openwrt官方提供的703N固件，经测试基本功能正常 但是白白浪费4M空间实在可惜，最终还是决定自己编译一份

## 编译Openwrt
-----------------------------------

> 已知信息：WiFi指示灯GPIO是0，高电平有效 网口状态灯是17，低电平有效 复位键是12，高电平有效

#### 使用docker-openwrt-buildroot进行编译


```shell
    docker run -it noonien/openwrt-buildroot bash  
    sudo apt-get update  
    sudo apt-get install git-core build-essential libssl-dev libncurses5-dev unzip gawk zlib1g-dev subversion mercurial gettext autoconf libtool libpcre3-dev asciidoc xmlto libev-dev libudns-dev libc-ares-dev automake libmbedtls-dev libsodium-dev  
```
    
```shell
    cd openwrt  
      
     ./scripts/feeds update -a  
      
     scripts/feeds install -a  
```

*   修改 `~/openwrt/target/linux/ar71xx/files/arch/mips/ath79/mach-tl-wr703n.c`
    
```C
    #define TL\_WR703N\_GPIO\_LED\_SYSTEM   0  
    #define TL\_WR703N\_GPIO\_BTN\_RESET    12  
```
     以及同文件 `gpio_led tl_wr703n_leds_gpio[]` 部分中
    
```C
    .active_low = 0,  
```
    
*   打开 `~/openwrt/target/linux/ar71xx/image/tiny-tp-link.mk` ，找到 `define Device/tl-wr703n-v1`。
    
*   将 `$(Device/tplink-4mlzma)` 中的 `4mlzma` 改成 `8mlzma` 就可以支持8MB固件编译（16MB同理）
    
*   在源代码目录下 `make menuconfig`
    
*   `Target System` 和 `Subtarget` 应该分别是Atheros `AR7xxx/AR9xxx`和`Devices with small flash`，`Target Profile`选择`TP-LINK TLWR703N v1`
    
*   启用 Web 管理界面 LuCI （记得选择为\[*\]而不是\[M\]，我们不需要编译ipk文件，直接整合进bin就行）
    
    `LuCI → Collections → 选中 luci`
    
*   添加 LuCI 中文支持
    
    `LuCI → Modules → Translations → 选中 Chinese (zh-cn)`
    
*   生成构建的配置文件，检查依赖
    
    `make defconfig`
    
*   编译，可加上 V=99 参数输出所有调试信息
    
    `make`
    
*   从 `openwrt/bin/target/ar71xx/tiny` 中取出 `openwrt-ar71xx-tiny-tl-wr703n-v1-squashfs-factory.bin` 刷入即可
    

### 附加内容：编译某不可描述软件

```shell
#自行去除空格  
git clone https://github.com/aa65535/openwrt-dist-luci.git package/openwrt-dist-luci  
git clone https://github.com/aa65535/openwrt-dns-forwarder.git package/dns-forwarder  
git clone https://github.com/Hill-98/luci-app-shad owsocks.git package/luci-app-shad owsocks  
git clone https://github.com/Hill-98/openwrt-shad owsocksr package/shad owsocksr-libev  
git clone https://github.com/Hill-98/openwrt-ckipver.git package/ckipver  

# 编译 po2lmo (如果有po2lmo可跳过)  
pushd package/luci-app-shad owsocksr/tools/po2lmo  
make && sudo make install  
# 选择要编译的包 dnsmasq-full curl wget coreutils-base64 bash bind-dig ckipver shad owsocksr-libev luci-app-sha dowsocks chinadns luci-app-chinadns dns-forwarder	luci-app-dns-forwarde ca-certificates openssl-util ca-bundle  
# 务必选择Using shared library from system   
# 提示 在menuconfig中按/可使用搜索  
make menuconfig
 ```