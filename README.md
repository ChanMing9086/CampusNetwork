# 破解校园网设备限制

----

## 我的配置

路由器:Xiaomi Mi Router 3G

编译路由器固件环境:Ubuntu 20.04.6 LTS (Focal Fossa)

执行固件刷写环境:Windows 10 pro 10.0.19041

网络环境:虚拟机内，科学上网

虚拟机:VMware Workstation Pro 17

SSH:XshellPlus-7.0.0031r

----

## 一、判断路由器是否支持输入OpenWrt系统

进入OpenWrt的[网站](https://openwrt.org/toh/start)，根据硬件列表：固件下载，查找你的路由器，如果在列表中可以找到你的路由器，说明你的路由器支持刷入，如果找不到，说明你的路由器不支持，就需要考虑换另一个芯片协议不同的路由器了



我这里截取了一小部分的小米路由器，在这个列表中，我看到了Xiaomi MiWiFi 3G，说明我的路由器是支持刷入的,如果不会判断自己的路由器支不支持，可以看列表中的[CPU](https://openwrt.org/zh/toh/views/toh_fwdownload),如果你的路由器芯片型号在列表中，那有很大概率是支持刷入的。

| Xiaomi | AIoT Router AC2350    |
| ------ | --------------------- |
| Xiaomi | AX3000T               |
| Xiaomi | AX3200                |
| Xiaomi | AX6S                  |
| Xiaomi | AX9000                |
| Xiaomi | Mi AIoT Router AX3600 |
| Xiaomi | MiWiFi 3G             |
| Xiaomi | Mi Router 4A (MIR4A)  |
| Xiaomi | Mi Router 4A (MIR4A)  |
| Xiaomi | Mi Router 4A (MIR4A)  |

-----

## 二、VM虚拟机安装Ubuntu(编译固件需要的系统环境)

### 1.系统镜像

Ubuntu官网，找到对应的Ubuntu版本下载，我选取的版本是[20.04.6](https://releases.ubuntu.com/20.04.6/)，因为这个版本相对于后续的几个版本来说，系统bug少，运行流畅稳定，如果你喜欢用新版本，可以在[发行版本](https://releases.ubuntu.com/)进行选择

补充:为什么不用其他的Linux系统？因为我没接触过，而且我觉得ubuntu系统，对新手比较友好

发行版本如下:

```
 Name                    Last modified      Size  Description 14.04.6/                2020-08-18 08:05    -   Ubuntu 14.04.6 LTS (Trusty Tahr)
 14.04/                  2020-08-18 08:05    -   Ubuntu 14.04.6 LTS (Trusty Tahr)
 16.04.7/                2020-08-18 17:01    -   Ubuntu 16.04.7 LTS (Xenial Xerus)
 16.04/                  2020-08-18 17:01    -   Ubuntu 16.04.7 LTS (Xenial Xerus)
 18.04.6/                2023-06-01 08:53    -   Ubuntu 18.04.6 LTS (Bionic Beaver)
 18.04/                  2023-06-01 08:53    -   Ubuntu 18.04.6 LTS (Bionic Beaver)
 20.04.6/                2023-03-22 14:31    -   Ubuntu 20.04.6 LTS (Focal Fossa)
 20.04/                  2023-03-22 14:31    -   Ubuntu 20.04.6 LTS (Focal Fossa)
 22.04.4/                2024-02-22 15:39    -   Ubuntu 22.04.4 LTS (Jammy Jellyfish)
 22.04/                  2024-02-22 15:39    -   Ubuntu 22.04.4 LTS (Jammy Jellyfish)
 23.10.1/                2023-12-04 18:38    -   Ubuntu 23.10 (Mantic Minotaur)
 23.10/                  2023-12-04 18:38    -   Ubuntu 23.10 (Mantic Minotaur)
 24.04/                  2024-04-25 17:26    -   Ubuntu 24.04 LTS (Noble Numbat)
 bionic/                 2023-06-01 08:53    -   Ubuntu 18.04.6 LTS (Bionic Beaver)
 focal/                  2023-03-22 14:31    -   Ubuntu 20.04.6 LTS (Focal Fossa)
 jammy/                  2024-02-22 15:39    -   Ubuntu 22.04.4 LTS (Jammy Jellyfish)
 mantic/                 2023-12-04 18:38    -   Ubuntu 23.10 (Mantic Minotaur)
 noble/                  2024-04-25 17:26    -   Ubuntu 24.04 LTS (Noble Numbat)
 streams/                2021-10-21 13:49    -   
 trusty/                 2020-08-18 08:05    -   Ubuntu 14.04.6 LTS (Trusty Tahr)
 xenial/                 2020-08-18 17:01    -   Ubuntu 16.04.7 LTS (Xenial Xerus)
```

点击你选的发行版本后，选择[下载](https://releases.ubuntu.com/20.04.6/ubuntu-20.04.6-desktop-amd64.iso)

如果你觉得下载慢，可以下载[种子文件]( ubuntu-20.04.6-desktop-amd64.iso.torrent),之后拖进迅雷，就可以下载了



### 2.配置虚拟机，安装Ubuntu

下载虚拟机，安装虚拟机，和配置虚拟机的操作，可以自行上网学习

安装Ubuntu系统，可以看我录制的视频



### 3.运行终端

在桌面空白处，鼠标右键，打开终端，Open in Terminal

#更新

```shell
sudo apt update
```

````shell
sudo apt full-upgrade  -y
````



#配置编译环境

```shell
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync
```



#克隆[lede](https://github.com/coolsnowwolf/lede)的源码

```shell
git clone https://github.com/coolsnowwolf/lede
```



#切换lede目录

```shell
cd lede
```



#克隆校园网的依赖模块

```shell
git clone https://github.com/EOYOHOO/UA2F.git package/UA2F
git clone https://github.com/EOYOHOO/rkp-ipid.git package/rkp-ipid
```



桌面，打开lede文件，里面有个feeds.conf.default文件，打开，内容如下

```ini
src-git packages https://github.com/coolsnowwolf/packages
src-git luci https://github.com/coolsnowwolf/luci
#src-git luci https://github.com/coolsnowwolf/luci.git;openwrt-23.05
src-git routing https://github.com/coolsnowwolf/routing
src-git telephony https://git.openwrt.org/feed/telephony.git
#src-git helloworld https://github.com/fw876/helloworld.git
#src-git oui https://github.com/zhaojh329/oui.git
#src-git video https://github.com/openwrt/video.git
#src-git targets https://github.com/openwrt/targets.git
#src-git oldpackages http://git.openwrt.org/packages.git
#src-link custom /usr/src/openwrt/custom-feed
```



#添加下面两行代码进去

```ini
src-git kenzo https://github.com/kenzok8/openwrt-packages
src-git small https://github.com/kenzok8/small
```

添加完后，内容是这样的，右上角记得save

```ini
src-git packages https://github.com/coolsnowwolf/packages
src-git luci https://github.com/coolsnowwolf/luci
#src-git luci https://github.com/coolsnowwolf/luci.git;openwrt-23.05
src-git routing https://github.com/coolsnowwolf/routing
src-git telephony https://git.openwrt.org/feed/telephony.git
#src-git helloworld https://github.com/fw876/helloworld.git
#src-git oui https://github.com/zhaojh329/oui.git
#src-git video https://github.com/openwrt/video.git
#src-git targets https://github.com/openwrt/targets.git
#src-git oldpackages http://git.openwrt.org/packages.git
#src-link custom /usr/src/openwrt/custom-feed
src-git kenzo https://github.com/kenzok8/openwrt-packages
src-git small https://github.com/kenzok8/small
```



#打开终端，执行更新feed模块命令

```shell
./scripts/feeds update -a
```

```shell
./scripts/feeds install -a
```



---

## 三、配置路由器，勾选模块

现在，你的终端应该是lede目录下，然后执行

```shell
cd lede
make menuconfig
```

你会看到一个菜单，下面的操作用方向键

第一行:Target System (Rockchip)，回车进入

这里是芯片开发商，选择你的芯片开发商，按y确任，然后退出

我的是:MediaTek Ralink MIPS  联发科

退出后，会显示Target System (MediaTek Ralink MIPS)

第二:Subtarget，找到你的芯片型号

我的是:Subtarget (MT7621 based boards)

第三:Target Profile，选择你的路由器，如果没有找到，说明上面选择的不正确

我的是:Target Profile (Xiaomi Mi Router 3G)

第四:Target Images，根据路由器的闪存和内存设置大小

我的内存设置:(128) Kernel partition size (in MiB)

我的闪存设置: (256) Root filesystem partition size (in MiB)

如果你没有看见Kernel partition size (in MiB)，没关系，默认就可以

----

同理，下面的设置也一样，没有看见，就往一级目录找，下面的第一个都是在一级目录，这些是防校园网检测的必须模块，y勾选

```ini
# kernel modules-Netfilter Extensions-kmod-ipt-ipopt
# kernel modules-Netfilter Extensions-kmod-ipt-u32
# kernel-modules-Other modules-kmod-rkp-ipid
# network-firewall-iptables-mod-conntrack-extra
# network-firewall-iptables-mod-filter
# network-firewall-iptables-mod-ipopt
# network-firewall-iptables-mod-u32
# network-Routing and Redirection-ua2f
```

勾选完模块，选择save保存，会显示.config

----------

## 四、编译固件

补充:这里需要用到科学上网，并且保持稳定，确保编译成功



#下载dl库

```shell
make download  -j8
```

#编译固件(1小时-2小时)

1是单线程

```shell
make V=s -j1 
```

编译完的输出路径:lede/bin/targets/ramips/mt7621

补充:你最后的芯片型号可能和我不同，因为我们的路由器不一样，所以最后的命名是你的芯片型号

我们需要的文件:

openwet-ramips-mt7621-xiaomi....sysupgrade.bin(文件大小最大)

相同的文件也是:

openwet-ramips-mt7621-xiaomi....kernel.bin

openwet-ramips-mt7621-xiaomi....roofs.bin

然后把这些文件复制到虚拟机外面(物理机)，自行创建个文件保存

-----

## 五、刷入breed

有些路由器刷入breed前，需要降级固件，关于如何降级固件，可以根据你的路由器去相应的官网搜索历史固件，查看教程，如果你的路由器官网没有降级教程，可以上[恩山论坛](https://www.right.com.cn/forum/)搜索

breed可以理解为window系统的PE，就是一个引导系统，通过这个类PE，就可以输入第三方路由器系统，比如梅林，老毛子

用一根网线，连接电脑网口和路由器的lan口，然后进路由器后台，复制当前网址的stock值，复制修改好stok的代码，替换到下面的CCCCCCCCC，全选粘贴到浏览器，回车。浏览器会显示 : {"code":0} ).，表示输入成功，如果显示其他代码，可能是你还没降级固件或者stok过期。也可以恢复出厂从试。

注:stock值只有纯数字，没有其它字符

```html
http://192.168.31.1/cgi-bin/luci/;stok=CCCCCCCCCCC/api/misystem/set_config_iotdev?bssid=Xiaomi&user_id=longdike&ssid=%0Acd%20%2Ftmp%0Acurl%20-o%20B%20-O%20https%3A%2F%2Fbreed.hackpascal.net%2Fr1286%2520%255b2020-10-09%255d%2Fbreed-mt7621-xiaomi-r3g.bin%20-k%20-g%0A%5B%20-z%20%22%24(sha256sum%20B%20%7C%20grep%20242d42eb5f5aaa67ddc9c1baf1acdf58d289e3f792adfdd77b589b9dc71eff85)%22%20%5D%20%7C%7C%20mtd%20-r%20write%20B%20Bootloader%0A
```

成功显示code:0后，60秒就会自动重启进breed，指示灯会从正常灯变异常灯，异常灯变正常灯，我这里不说颜色，因为每个路由器的指示灯不一样。

本教程借鉴了恩山作者[jinglei207](https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=4066963&highlight=%E4%B8%80%E9%94%AE%E5%88%B7)的教程，不明白的可以去他的帖子加深印象

成功进去breed后，

固件更新->勾选固件，选择文件(openwet-ramips-mt7621-xiaomi....sysupgrade.bin)

同理其他的，如果有就勾选，并且选择相应的文件

kernel文件就选...kernel.bin，roofs文件就选roofs.bin

有的roofs文件选了后会提示校验失败，如果失败了，不勾选就行，至于为什么失败，我的能力有限。。。

勾选完后，闪存布局可以是自动检测，也可以选你的路由器型号

重启

补充:如果想回原厂系统，路由器断电，用卡针顶住reset，然后接电，长顶5秒后，看到灯闪烁，就可以松开了，进入breed，选择固件更新，选择原厂固件miwifi_rm2100_firmware_d6asd_breed.bin，可以参考这个格式，闪存布局选择原厂，上传

如果你是小米的，先进环境变量山，删除这一行

这行是检验是否为官方固件

| nomal_firware_md5 |      |
| ----------------- | ---- |

--------------------

## 六、配置规则

如果你刷入成功了，那么恭喜你，距离不远了

现在，按照学校网口-路由器wan口，路由器lan口-电脑网口，接入两根网线

路由器通电，进入OpenWrt,一般网址是192.168.1.1，有的网址是10.0.0.1，如果这两个还进不去的话，上网查阅这款路由器刷入openwrt后的网址，还进不去的话，可能是没有刷成功，可以尝试重新刷写一次，如果还不行，去恩山请神

| 用户名:root | 默认密码:password |
| ----------- | ----------------- |



### 1.NTP服务器

进入 系统设置, 勾选

 Enable NTP client（启用 NTP 客户端）

 Provide NTP server（作为 NTP 服务器提供服务）

NTP server candidates（候选 NTP 服务器）四个框分别填写 

| ntp1.aliyun.com         |
| ----------------------- |
| time1.cloud.tencent.com |
| stdtime.gov.hk          |
| pool.ntp.org            |



### 2.防火墙自定义规则

找到防火墙一栏，打开自定义规则，把下面的规则全选粘贴进去，重启防火墙

```sql
iptables -t nat -A PREROUTING -p udp --dport 53 -j REDIRECT --to-ports 53

iptables -t nat -A PREROUTING -p tcp --dport 53 -j REDIRECT --to-ports 53

# 通过 rkp-ipid 设置 IPID

# 若没有加入rkp-ipid模块，此部分不需要加入

iptables -t mangle -N IPID_MOD

iptables -t mangle -A FORWARD -j IPID_MOD

iptables -t mangle -A OUTPUT -j IPID_MOD

iptables -t mangle -A IPID_MOD -d 0.0.0.0/8 -j RETURN

iptables -t mangle -A IPID_MOD -d 127.0.0.0/8 -j RETURN

iptables -t mangle -A IPID_MOD -d 10.0.0.0/8 -j RETURN

iptables -t mangle -A IPID_MOD -d 172.16.0.0/12 -j RETURN

iptables -t mangle -A IPID_MOD -d 192.168.0.0/16 -j RETURN

iptables -t mangle -A IPID_MOD -d 255.0.0.0/8 -j RETURN

iptables -t mangle -A IPID_MOD -j MARK --set-xmark 0x10/0x10

# 防时钟偏移检测

iptables -t nat -N ntp_force_local

iptables -t nat -I PREROUTING -p udp --dport 123 -j ntp_force_local

iptables -t nat -A ntp_force_local -d 0.0.0.0/8 -j RETURN

iptables -t nat -A ntp_force_local -d 127.0.0.0/8 -j RETURN

iptables -t nat -A ntp_force_local -d 192.168.0.0/16 -j RETURN

iptables -t nat -A ntp_force_local -s 192.168.0.0/16 -j DNAT --to-destination 192.168.1.1

# 通过 iptables 修改 TTL 值 数字为需要的修改的ttl值

iptables -t mangle -A POSTROUTING -j TTL --ttl-set 64

# iptables 拒绝 AC 进行 Flash 检测

iptables -I FORWARD -p tcp --sport 80 --tcp-flags ACK ACK -m string --algo bm --string " src=\"http://1.1.1." -j DROP
```



### 3.使用ssh工具开启ua2f配置

打开xshell，主机名就是路由器的ip地址，用户身份验证，就是输入root，和password，如果你刚刚在路由器后台修改了用户名和密码，这里相同

比如我的就是填写

主机:192.168.1.1 

用户:root password



打开终端

#检查ssh状态，如果开启了，就可以执行下面操作

```shell
sudo systemctl status ssh
```



#如果没有开启，先执行这行，开启ssh

```shell
sudo systemctl start ssh
```



#开机自启

```shell
uci set ua2f.enabled.enabled=1
```



#自动配置防火墙(默认开启)(建议开启）

```shell
uci set ua2f.firewall.handle_fw=1
uci set ua2f.firewall.handle_tls=1
uci set ua2f.firewall.handle_mmtls=1
uci set ua2f.firewall.handle_intranet=1
```



#保存配置

```shell
uci commit ua2f
```



#开机自启

```shell
service ua2f enable
```



#启动ua2f

```shell
service ua2f start
```



#手动关闭ua2f

```shell
service ua2f stop
```



------------------------

## 七、检验UA2F

最后，进入[检测网站](http://ua.233996.xyz:1234/)，如果和我一样，全是F，说明成功了，这时候就可以喊你舍友也连入校园网，你就会发现，一个账号可以多台设备，而且只要一个设备认证了，其他设备接入校园网时，就不会弹出网页认证

```html
你的真实UA是(服务器获取的UA)
FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
你的浏览器UA是
FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
你的IP是(注意是否走代理了)
192..*.
标准端口测试
非标准端口测试(1234)
TLS测试
```



-------------------------

## 尾言

总的来说，本教程操作难度并不大，如果你真的下定决心破解校园网，实现多台设备，我相信，看完这篇教程，再结合你的自行学习，肯定也可以办到的。成功的关键在于持之以恒的探索和实践。建议在实际操作中细致观察每一步，适时调整方法。通过不断尝试与学习，你将能更深入地理解网络的本质，最终达到你的目标。

请务必注意遵循相关法律法规，确保行为的合规性

-----------

# 额外补充

## 参考资料(写本教程所参考的其他教程)

[openwrt编译校园网防检测固件（例r2s）](https://y5hwpw3fsi.feishu.cn/docx/UO0wdHReDoUdewxwlpGckSjin3d)



[[AC2100(RM2100)]小米 红米【AC2100】一键刷BREED【30秒刷完】小白帅小伙专用 检查坏块 | 无需Telnet](https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=4066963&highlight=%E4%B8%80%E9%94%AE%E5%88%B7)



[关于某大学校园网共享上网检测机制的研究与解决方案](https://blog.sunbk201.site/posts/crack-campus-network)



[openwrt校园网防检测固件编译教程，新路由3为例](  https://www.bilibili.com/video/BV1fN411n7d1/?spm_id_from=333.337.search-card.all.click&vd_source=b816429690fadda929b54cde297193b5)



[校园网防检测！软路由固件编译教程](https://www.bilibili.com/video/BV1qM411w7W5/?share_source=copy_web&vd_source=8f40f0fe12ad6588eabef842882a5b7c)

-----------

## 上网检测机制

### 基于 IPv4 数据包包头内的 TTL 字段的检测

```html
校园网中，基于IPv4数据包头内TTL字段的检测原理主要涉及以下几个方面：

1. TTL字段的作用

生存时间：TTL（Time to Live）字段用于限制数据包在网络中的生存时间，防止数据包无限循环。每经过一个路由器，TTL值减少1，当TTL值减至0时，数据包被丢弃。
跳数控制：通过设置初始TTL值，可以控制数据包允许经过的最大路由跳数。

2. 检测原理

TTL值的初始设置：数据包在源主机发送时，TTL值通常设定为特定的初始值（如64、128或255），具体值取决于操作系统或应用。
路由器的处理：每经过一个路由器，TTL值减1。当数据包到达目标主机时，可以通过比较接收到的TTL值与原始TTL值推算出经过的跳数。

3. 检测方法

Ping命令：发送ICMP Echo请求并记录接收到的TTL值。通过比较原始TTL值和接收到的TTL值，计算跳数。
Traceroute工具：逐跳发送数据包，使用不同的TTL值（从1开始递增），记录每个路由器的响应，构建网络路径。  
```



### 基于 HTTP 数据包请求头内的 User-Agent 字段的检测

```html
校园网中，基于HTTP数据包请求头内的User-Agent字段的检测原理主要包括以下几个方面：

1. User-Agent字段的定义

用户代理：User-Agent字段包含客户端软件的信息，如浏览器类型、操作系统、设备类型等。它用于告诉服务器请求来自哪个客户端。

2. 检测原理

请求识别：当用户通过浏览器或应用程序发送HTTP请求时，User-Agent字段会随请求发送。服务器可以通过解析该字段来识别请求来源。
数据分析：通过收集和分析User-Agent字段的信息，网络管理员可以了解用户使用的设备和浏览器类型，识别潜在的安全风险。

3. 检测方法

日志记录：服务器可以记录所有HTTP请求的头信息，包括User-Agent字段，供后续分析。
数据挖掘：使用工具和脚本自动化分析User-Agent数据，以识别常见的浏览器、操作系统版本及其趋势。
```



### DPI (Deep Packet Inspection) 深度包检测技术

```ht
在校园网中，DPI（Deep Packet Inspection）深度包检测技术的应用主要体现在以下几个方面：

1. 网络流量管理

带宽优化：DPI可以识别不同类型的流量（如视频、游戏、社交媒体），帮助网络管理员进行带宽分配和优化，确保关键应用获得优先资源。

2. 安全防护

恶意内容检测：通过深入分析数据包，DPI可以识别和阻止恶意软件、病毒和入侵尝试，增强网络安全。
异常行为监测：实时监控流量，识别异常活动，及时响应潜在的安全威胁。

3. 合规性监控

政策执行：DPI可用于监测网络使用情况，确保用户遵循学校的网络使用政策，识别不当行为（如非法下载或访问不当内容）。

4. 用户体验提升

流量分类：根据应用类型优化网络流量，提高用户在访问高需求应用时的体验，例如在线学习和视频会议。

5. 实施注意事项

隐私考虑：在实施DPI时需遵循相关法律法规，保护用户隐私，避免不当监控。
加密流量挑战：随着HTTPS加密的普及，DPI在处理加密流量时可能受到限制，需采用适当技术确保有效检测。
```

### 基于 IPv4 数据包包头内的 Identification 字段的检测

```html
在校园网中，基于IPv4数据包头内的Identification字段的检测原理涉及数据包的唯一标识和分片重组。以下是对该字段的详细解析：

1. Identification字段的定义

作用：IPv4数据包头中的Identification字段用于唯一标识一个数据包，尤其是在分片的情况下。它是一个16位的字段，当一个数据包被分片时，所有的片段都将使用相同的Identification值，以便接收方能够正确地将这些片段重组为完整的数据包。

2. 检测原理

分片与重组：当一个IP数据包过大而无法通过某个网络段时，它将被分片。Identification字段确保所有片段可以正确识别和重组。
唯一性：每个数据包的Identification字段在同一源主机中必须唯一，以防止不同数据包的片段混淆。

3. 检测方法

数据包捕获：通过使用网络分析工具（如Wireshark）捕获和分析数据包，检查Identification字段的值。
分片检测：检测相同Identification字段的多个数据包片段，以验证它们是否来自同一原始数据包，确保重组的完整性。
```



### 基于网络协议栈时钟偏移的检测技术

```html
在校园网中，基于网络协议栈时钟偏移的检测技术主要用于监测和校正网络设备之间的时间同步。以下是该技术的核心内容：

1. 时钟偏移的定义

时钟偏移：指网络设备之间时钟的差异，可能导致数据包传输顺序混乱、协议失效等问题。

2. 检测原理

网络时间协议（NTP）：通过使用NTP等协议，定期与时间服务器同步时间，检测并修正时钟偏移。
时间戳比较：在数据包中嵌入时间戳，通过比较接收到的时间戳与本地时间，识别时钟偏移。

3. 检测方法

NTP监控：监测NTP同步的状态，记录同步延迟和偏移量，确保设备时间的准确性。
数据包分析：通过捕获和分析数据包中的时间戳信息，检查时钟偏移情况。
```



### Flash Cookie 检测技术

```html
在校园网环境中，Flash Cookie（也称为本地共享对象，LSO）检测技术主要用于识别和管理存储在用户设备上的Flash Cookie。以下是该技术的关键点：

1. Flash Cookie的定义

Flash Cookie：是一种由Adobe Flash Player创建和存储的小型数据文件，用于保存用户的偏好设置和网站数据。与传统的HTTP Cookies不同，Flash Cookie可以存储更多数据，并且在删除普通Cookies时不会被清除。

2. 检测原理

存储位置：Flash Cookies存储在用户的设备中，通常在特定的文件夹下，可以通过特定工具进行访问和分析。
数据分析：检测工具可以扫描用户设备，识别Flash Cookie的存在和内容，以便了解用户活动和偏好。

3. 检测方法

工具使用：利用专门的检测工具（如Adobe提供的管理面板或其他第三方工具）来检查和管理Flash Cookies。
网络监控：通过网络流量分析，监测与Flash相关的请求和响应，以识别Flash Cookie的使用情况。
```

-------


