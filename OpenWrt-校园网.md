# OpenWrt-校园网

路由器:Xiaomi Mi Router 3G

编译路由器固件环境:Ubuntu 20.04.6 LTS (Focal Fossa)

执行刷写环境:Microsoft Windows 10 pro 10.0.19041 

网络环境:科学上网

虚拟机:VMware Workstation Pro 17

SSH:xshell

----

## 判断路由器能否刷入OpenWrt

打开OpenWrt的官网，点击下面链接，进入的硬件列表页面，根据列表，寻找你的路由器，如果在列表中可以找到你的路由器，说明你的路由器支持刷入，如果列表上没有显示你的路由器，说明你的路由器无法输入，具体原因是路由器里的芯片不支持运行OpenWrt

https://openwrt.org/zh/toh/views/toh_fwdownload

我这里截取了一小部分的小米路由器，在这个列表中，我看到了我的路由器Xiaomi MiWiFi 3G，所以我的路由器是支持输入的，如果不确定是否是自己的路由器，可以看到芯片列generic，如果你的芯片对的上，那说明是你的路由器了。同理，如果你知道你的路由器的芯片型号，芯片列generic中显示你的芯片型号，说明你的路由器可以刷入

| Xiaomi | AIoT Router AC2350                 |                      | [23.05.0](https://openwrt.org/releases/23.05.0)   | USB IoT radio    | Qualcomm Atheros QCA9563       | [ath79](https://openwrt.org/docs/techref/targets/ath79)      | generic | [Factory image](https://downloads.openwrt.org/releases/23.05.0/targets/ath79/generic/openwrt-23.05.0-ath79-generic-xiaomi_aiot-ac2350-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.0/targets/ath79/generic/openwrt-23.05.0-ath79-generic-xiaomi_aiot-ac2350-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ath79/generic/openwrt-ath79-generic-xiaomi_aiot-ac2350-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ath79/generic/openwrt-ath79-generic-xiaomi_aiot-ac2350-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_aiot_router_ac2350) |
| ------ | ---------------------------------- | -------------------- | ------------------------------------------------- | ---------------- | ------------------------------ | ------------------------------------------------------------ | ------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Xiaomi | AX3000T                            |                      | [snapshot](https://openwrt.org/releases/snapshot) |                  | MediaTek MT7981B               | [mediatek](https://openwrt.org/docs/techref/targets/mediatek) | filogic |                                                              |                                                              | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/mediatek/filogic/) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/mediatek/filogic/openwrt-mediatek-filogic-xiaomi_mi-router-ax3000t-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_ax3000t) |
| Xiaomi | AX3200                             |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7622B               | [mediatek](https://openwrt.org/docs/techref/targets/mediatek) | mt7622  | [Factory image](http://downloads.openwrt.org/releases/23.05.3/targets/mediatek/mt7622/openwrt-23.05.3-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-factory.bin) | [Sysupgrade image](http://downloads.openwrt.org/releases/23.05.3/targets/mediatek/mt7622/openwrt-23.05.3-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-sysupgrade.bin) | [Factory snapshot image](http://downloads.openwrt.org/snapshots/targets/mediatek/mt7622/openwrt-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-factory.bin) | [Factory sysupgrade image](http://downloads.openwrt.org/snapshots/targets/mediatek/mt7622/openwrt-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_ax3200)  |
| Xiaomi | AX6S                               |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7622B               | [mediatek](https://openwrt.org/docs/techref/targets/mediatek) | mt7622  | [Factory image](http://downloads.openwrt.org/releases/23.05.3/targets/mediatek/mt7622/openwrt-23.05.3-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-factory.bin) | [Sysupgrade image](http://downloads.openwrt.org/releases/23.05.3/targets/mediatek/mt7622/openwrt-23.05.3-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-sysupgrade.bin) | [Factory snapshot image](http://downloads.openwrt.org/snapshots/targets/mediatek/mt7622/openwrt-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-factory.bin) | [Factory sysupgrade image](http://downloads.openwrt.org/snapshots/targets/mediatek/mt7622/openwrt-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_ax6s)    |
| Xiaomi | AX9000                             |                      | [23.05.2](https://openwrt.org/releases/23.05.2)   |                  | Qualcomm Atheros IPQ8072A      | [qualcommax](https://openwrt.org/docs/techref/targets/qualcommax) | ipq807x | [Factory image](https://downloads.openwrt.org/releases/23.05.1/targets/ipq807x/generic/openwrt-23.05.1-ipq807x-generic-xiaomi_ax9000-initramfs-factory.ubi) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.1/targets/ipq807x/generic/openwrt-23.05.1-ipq807x-generic-xiaomi_ax9000-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/qualcommax/ipq807x/openwrt-qualcommax-ipq807x-xiaomi_ax9000-initramfs-factory.ubi) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/qualcommax/ipq807x/openwrt-qualcommax-ipq807x-xiaomi_ax9000-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_ax9000)  |
| Xiaomi | Mi AIoT Router AX3600              |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   | NSS acceleration | Qualcomm IPQ8071A              |                                                              | ipq807x | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ipq807x/generic/openwrt-23.05.3-ipq807x-generic-xiaomi_ax3600-initramfs-factory.ubi) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ipq807x/generic/openwrt-23.05.3-ipq807x-generic-xiaomi_ax3600-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/qualcommax/ipq807x/openwrt-qualcommax-ipq807x-xiaomi_ax3600-initramfs-factory.ubi) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/qualcommax/ipq807x/openwrt-qualcommax-ipq807x-xiaomi_ax3600-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_ax3600)  |
| Xiaomi | Mi Router 3 Pro                    |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621AT              | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-3-pro-squashfs-factory.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-3-pro-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-3-pro-squashfs-factory.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-3-pro-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_3_pro) |
| Xiaomi | Mi Router 4A (MIR4A)               | 100M                 | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7628DAN             | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt76x8  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_mi-router-4a-100m-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_mi-router-4a-100m-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_mi-router-4a-100m-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_mi-router-4a-100m-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_4a_100m) |
| Xiaomi | Mi Router 4A (MIR4A)               | Gbit v2              | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621AT              | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-4a-gigabit-v2-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-4a-gigabit-v2-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-4a-gigabit-v2-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-4a-gigabit-v2-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_4a_mir4a_gbit_v2) |
| Xiaomi | Mi Router 4A (MIR4A)               | Gigabit Edition v1   | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621AT              | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-4a-gigabit-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-4a-gigabit-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-4a-gigabit-initramfs-kernel.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-4a-gigabit-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_4a_gbit) |
| Xiaomi | Mi Router 4A (R4AC)                | 100M (International) | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7628DAN             | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt76x8  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_mi-router-4a-100m-intl-initramfs-kernel.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_mi-router-4a-100m-intl-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_mi-router-4a-100m-intl-initramfs-kernel.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_mi-router-4a-100m-intl-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_r4ac_international_100m) |
| Xiaomi | Mi Router 4C                       |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7628DAN             | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt76x8  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_mi-router-4c-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_mi-router-4c-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_mi-router-4c-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_mi-router-4c-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_4c) |
| Xiaomi | Mi Router 4Q                       |                      | [23.05.0](https://openwrt.org/releases/23.05.0)   |                  | Qualcomm Atheros QCA9561       | [ath79](https://openwrt.org/docs/techref/targets/ath79)      | generic | [Factory image](https://downloads.openwrt.org/releases/23.05.0/targets/ath79/generic/openwrt-23.05.0-ath79-generic-xiaomi_mi-router-4q-initramfs-kernel.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.0/targets/ath79/generic/openwrt-23.05.0-ath79-generic-xiaomi_mi-router-4q-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ath79/generic/openwrt-ath79-generic-xiaomi_mi-router-4q-initramfs-kernel.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ath79/generic/openwrt-ath79-generic-xiaomi_mi-router-4q-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_4q) |
| Xiaomi | Mi Router AC2100                   |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621A               | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-ac2100-squashfs-kernel1.bin), [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-ac2100-squashfs-rootfs0.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-ac2100-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-ac2100-squashfs-kernel1.bin), [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-ac2100-squashfs-rootfs0.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-ac2100-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_ac2100) |
| Xiaomi | Mi Router CR6606                   |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621AT              | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-cr6606-squashfs-firmware.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-cr6606-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-cr6606-squashfs-firmware.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-cr6606-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_cr6606) |
| Xiaomi | Mi Router CR6608                   |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621AT              | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-cr6608-squashfs-firmware.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-cr6608-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-cr6608-squashfs-firmware.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-cr6608-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_cr6608) |
| Xiaomi | Mi Router CR6609                   |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621AT              | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-cr6609-squashfs-firmware.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-cr6609-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-cr6609-squashfs-firmware.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-cr6609-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_cr6609) |
| Xiaomi | Mi WiFi Mini                       | v1                   | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7620A               | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7620  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7620/openwrt-23.05.3-ramips-mt7620-xiaomi_miwifi-mini-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7620/openwrt-23.05.3-ramips-mt7620-xiaomi_miwifi-mini-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7620/openwrt-ramips-mt7620-xiaomi_miwifi-mini-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7620/openwrt-ramips-mt7620-xiaomi_miwifi-mini-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mini_v1) |
| Xiaomi | Mi WiFi Range Extender AC1200 RA75 |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | mt7628DAN                      | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt76x8  | [Factory image](https://archive.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_mi-ra75-squashfs-sysupgrade.bin) | [Sysupgrade image](https://archive.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_mi-ra75-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_mi-ra75-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_mi-ra75-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_wifi_range_extender_ac1200_ra75) |
| Xiaomi | MiWifi 3C                          |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7628AN              | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt76x8  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_miwifi-3c-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_miwifi-3c-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_miwifi-3c-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_miwifi-3c-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_miwifi_3c) |
| Xiaomi | MiWiFi 3G                          | v1                   | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621AT              | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/22.03.3/targets/ramips/mt7621/openwrt-22.03.3-ramips-mt7621-xiaomi_mi-router-3g-squashfs-kernel1.bin), [Factory image](https://downloads.openwrt.org/releases/22.03.0/targets/ramips/mt7621/openwrt-22.03.0-ramips-mt7621-xiaomi_mi-router-3g-squashfs-rootfs0.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-3g-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-3g-squashfs-kernel1.bin), [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-3g-squashfs-rootfs0.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-3g-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_miwifi_3g) |
| Xiaomi | MiWiFi 3G                          | v2                   | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621A               | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-3g-v2-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-3g-v2-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-3g-v2-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-3g-v2-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_miwifi_3g_v2) |
| Xiaomi | MiWiFi Nano                        |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7628                | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt76x8  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_miwifi-nano-squashfs-sysupgrade.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt76x8/openwrt-23.05.3-ramips-mt76x8-xiaomi_miwifi-nano-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_miwifi-nano-squashfs-sysupgrade.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt76x8/openwrt-ramips-mt76x8-xiaomi_miwifi-nano-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_miwifi_nano) |
| Xiaomi | MiWiFi R4                          | v1                   | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621A               | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | MT7621  | [Factory image](https://downloads.openwrt.org/releases/22.03.3/targets/ramips/mt7621/openwrt-22.03.3-ramips-mt7621-xiaomi_mi-router-4-squashfs-kernel1.bin), [Factory image](https://downloads.openwrt.org/releases/22.03.0/targets/ramips/mt7621/openwrt-22.03.0-ramips-mt7621-xiaomi_mi-router-4-squashfs-rootfs0.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_mi-router-4-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-4-squashfs-kernel1.bin), [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-4-squashfs-rootfs0.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_mi-router-4-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_miwifi_r4) |
| Xiaomi | Redmi AX6                          |                      | [snapshot](https://openwrt.org/releases/snapshot) |                  | Qualcomm IPQ8071A / QCA8074 V2 | [qualcommax](https://openwrt.org/docs/techref/targets/qualcommax) | ipq807x | [Factory image](https://downloads.openwrt.org/releases/23.05.0/targets/ipq807x/generic/openwrt-23.05.0-ipq807x-generic-redmi_ax6-initramfs-factory.ubi) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.0/targets/ipq807x/generic/openwrt-23.05.0-ipq807x-generic-redmi_ax6-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/qualcommax/ipq807x/openwrt-qualcommax-ipq807x-redmi_ax6-initramfs-factory.ubi) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/qualcommax/ipq807x/openwrt-qualcommax-ipq807x-redmi_ax6-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_redmi_ax6) |
| Xiaomi | Redmi AX6000                       |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7986A               | [mediatek](https://openwrt.org/docs/techref/targets/mediatek) | filogic | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/mediatek/filogic/openwrt-23.05.3-mediatek-filogic-xiaomi_redmi-router-ax6000-stock-initramfs-factory.ubi), [Factory image](fhttps://downloads.openwrt.org/releases/23.05.3/targets/mediatek/filogic/openwrt-23.05.3-mediatek-filogic-xiaomi_redmi-router-ax6000-ubootmod-initramfs-factory.ubi) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/mediatek/filogic/openwrt-23.05.3-mediatek-filogic-xiaomi_redmi-router-ax6000-stock-squashfs-sysupgrade.bin), [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/mediatek/filogic/openwrt-23.05.3-mediatek-filogic-xiaomi_redmi-router-ax6000-ubootmod-squashfs-sysupgrade.itb) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/mediatek/filogic/openwrt-mediatek-filogic-xiaomi_redmi-router-ax6000-stock-initramfs-factory.ubi) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/mediatek/filogic/openwrt-mediatek-filogic-xiaomi_redmi-router-ax6000-stock-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_redmi_ax6000) |
| Xiaomi | Redmi Router AC2100                |                      | [23.05.3](https://openwrt.org/releases/23.05.3)   |                  | MediaTek MT7621A               | [ramips](https://openwrt.org/docs/techref/targets/ramips)    | mt7621  | [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_redmi-router-ac2100-squashfs-kernel1.bin), [Factory image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_redmi-router-ac2100-squashfs-rootfs0.bin) | [Sysupgrade image](https://downloads.openwrt.org/releases/23.05.3/targets/ramips/mt7621/openwrt-23.05.3-ramips-mt7621-xiaomi_redmi-router-ac2100-squashfs-sysupgrade.bin) | [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_redmi-router-ac2100-squashfs-kernel1.bin), [Factory snapshot image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_redmi-router-ac2100-squashfs-rootfs0.bin) | [Factory sysupgrade image](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-xiaomi_redmi-router-ac2100-squashfs-sysupgrade.bin) | [Edit](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_redmi_router_ac2100) |

-----

## 虚拟机安装Ubuntu

打开Ubuntu官网，找到对应的Ubuntu版本，点击下载，我这里选取的版本是20.04.6，因为这个版本稳定，不过XZ后门的问题，不知道这个版本解决没有，我没有去了解。第一个链接是下载我用的版本，如果你喜欢用新版本，可以用第二个链接，第二个链接显示了所以版本的发行

https://releases.ubuntu.com/20.04.6/

https://releases.ubuntu.com/

第二个链接如下图

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

点击你选的发行版本后，选择[ ubuntu-20.04.6-desktop-amd64.iso](https://releases.ubuntu.com/20.04.6/ubuntu-20.04.6-desktop-amd64.iso)下载

如果你觉得浏览器下载慢，可以下载种子文件，[ ubuntu-20.04.6-desktop-amd64.iso.torrent](https://releases.ubuntu.com/20.04.6/ubuntu-20.04.6-desktop-amd64.iso.torrent)下载完后，拖进迅雷，就能识别下载了

我有迅雷会员，所以我是下载种子文件，然后拖进迅雷下载

------------

如果你看到这里，那么恭喜你，接下来就是吃操作的时候了，上面的部分只是简单的下载文件而已，现在，你需要掌握虚拟机安装镜像和Linux命令，如果你不会，自行学习。Linux命令不会的，无脑复制粘贴下面的就行，基本命令不解释

下表格是我的配置，不需要和我一样也可以，确保系统能稳定运行就行

| 内存       | 4GB  |
| ---------- | ---- |
| 处理器     | 2    |
| 硬盘(SCSI) | 30GB |
| 网络适配器 | NAT  |

进入系统后，打开终端，执行命令前，需要科学上网，如果是物理机可以科学上网，网络类型选择桥接（十分不建议这么做，裸奔操作），如果你有可以运行在Linxu系统的科学上网，选择NAT模式即可。如果你没有科学上网，可以试试切换国内源，我没有试过用国内源，不知道行不行通，切换国内源的方法，自行学习。

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

#克隆lede的源码，lede是一位编译路由器固件的大神，作者主页

https://github.com/coolsnowwolf/lede

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

打开文件系统，打开lede文件，里面有个feeds.conf.default文件，打开，内容如下

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

添加完后，内容是这样的

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

#打开终端，执行更新feed模块命令，一行一行复制执行，不要急

```shell
./scripts/feeds update -a
./scripts/feeds install -a
```

------------------

## 确认路由器的名称、芯片型号、闪存和内存

为什么写这个？因为等会编译路由器固件时需要用的到，所以先收集好你的路由器的这些信息，这里就没什么可说的，自行搜索你的路由器信息

---

## 上网检测机制

已知情况下，常见的检测技术有：

- 基于 IPv4 数据包包头内的 TTL 字段的检测
- 基于 HTTP 数据包请求头内的 User-Agent 字段的检测
- DPI (Deep Packet Inspection) 深度包检测技术
- 基于 IPv4 数据包包头内的 Identification 字段的检测
- 基于网络协议栈时钟偏移的检测技术
- Flash Cookie 检测技术

我这里写第二的解决方案，其余的解决方案我会在教程的末端放上链接

## 抓包

这里可以跳过，写这个是验证学校的上网检测机制是不是第二条，如果是网页认证的方式，一个账号2-3设备，极大可能是

首先打开你的认证页面，下线，按键F12，点击网络，然后点击登录，会显示以下内容，...是省略后面的部分

| quickauth.do?...        |
| ----------------------- |
| logout.html?...         |
| font-awesome.min.css... |
| jquery.js...            |
| ...                     |

选择第二个，logout.html?...，右键->复制->以cURL(cmd)格式复制，然后粘贴在记事本，看到这部分，可以看见Windows NT 10.0，这就是表头，意思说，若发现同时出现例如Windows NT 10.0 的字段，则判定存在多设备上网

```cmd
"User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36" ^
```

解决方案就是模拟表头，也就是将表头模拟成路由器的，而不是你的电脑或者手机，这样检测到的，也只是一台路由器上了网，不管你的电脑和手机连接到路由器的wifi，也是算路由器登录，这样就不存在多个设备断的问题。使用的模块是ua2f，接下来就讲

-------------------------

## 路由器选取和勾选模块

现在，你的终端应该是lede目录下，然后执行

```shell
make menuconfig
```

你会看到一个菜单，下面的操作用方向键

第一，Target System (Rockchip)，回车进入

这里是芯片开发商，选择你的芯片开发商，按y确任，然后退出

我的是:MediaTek Ralink MIPS  联发科

退出后，会显示Target System (MediaTek Ralink MIPS)

第二，打开Subtarget，找到你的芯片型号

我的是:Subtarget (MT7621 based boards)

第三，打开Target Profile，选择你的路由器，如果没有找到，说明上面选择的不正确

我的是:Target Profile (Xiaomi Mi Router 3G)

第四，打开Target Images，根据路由器的闪存和内存设置大小

我的内存设置:(128) Kernel partition size (in MiB)

我的闪存设置: (256) Root filesystem partition size (in MiB)

如果你没有看见Kernel partition size (in MiB)，没关系，不用设置这一项也行

----

同理，下面的设置也一样，没有看见就往下找，这些是防校园网检测的必须模块

```ini
# kernel-modules->Other modules->kmod-rkp-ipid
# kernel modules->Netfilter Extensions->kmod-ipt-u32
# kernel modules->Netfilter Extensions->kmod-ipt-ipopt
# network->Routing and Redirection->ua2f
# network->firewall->iptables-mod-filter
# network->firewall->iptables-mod-ipopt
# network->firewall->iptables-mod-u32
# network->firewall->iptables-mod-conntrack-extra
```

勾选完模块，选择save保存

----------

## 本地编译固件(保持科学上网状态稳定)

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

我们需要的文件:

openwet-ramips-mt7621-xiaomi....sysupgrade.bin(文件大小最大)

相同的文件也是:

openwet-ramips-mt7621-xiaomi....kernel.bin

openwet-ramips-mt7621-xiaomi....roofs.bin

然后把这些文件复制到物理机，自行创建个文件保存

-----

## 刷入breed

有些路由器刷入breed前，需要降级固件，也是会在教程的底端放链接

breed可以理解为window系统的bios，就是一个引导系统，有了这个引导系统，就可以刷任何的系统，比如梅林，老毛子，还有本教程的openwrt

用一根网线，连接电脑和路由器的lan，然后电脑上这个路由器的后台，复制当前网址的stock值，复制修改好stok的代码，替换到下面的CCCCCCCCC，全选粘贴到浏览器，回车。浏览器会显示 : {"code":0} ).，表示输入成功，如果显示其他代码，可能是你还没降级固件或者stok过期。也可以恢复出厂从试。

注:stock值只有纯数字，没有其它字符

```html
http://192.168.31.1/cgi-bin/luci/;stok=CCCCCCCCCCC/api/misystem/set_config_iotdev?bssid=Xiaomi&user_id=longdike&ssid=%0Acd%20%2Ftmp%0Acurl%20-o%20B%20-O%20https%3A%2F%2Fbreed.hackpascal.net%2Fr1286%2520%255b2020-10-09%255d%2Fbreed-mt7621-xiaomi-r3g.bin%20-k%20-g%0A%5B%20-z%20%22%24(sha256sum%20B%20%7C%20grep%20242d42eb5f5aaa67ddc9c1baf1acdf58d289e3f792adfdd77b589b9dc71eff85)%22%20%5D%20%7C%7C%20mtd%20-r%20write%20B%20Bootloader%0A
```

成功显示code:0后，60秒就会自动重启进breed，指示灯会从正常灯变异常灯，异常灯变正常灯，我这里不说颜色，因为每个路由器的指示灯不一样。

想刷不死breed的自行学习，链接放底端，

成功进去breed后，

固件更新->勾选固件，选择文件(openwet-ramips-mt7621-xiaomi....sysupgrade.bin)

同理其他的，如果有就勾选，并且选择相应的文件

kernel文件就选...kernel.bin，kernel1文件就选...kernel1.bin

勾选完后，闪存布局可以是自动检测，也可以选你的路由器型号

重启

注:如果想回原厂系统，路由器断电，用卡针顶住reset，然后接电，长顶5秒后，看到灯闪烁，就可以松开了，进入breed，选择固件更新，选择原厂固件miwifi_rm2100_firmware_d6asd_breed.bin，可以参考这个格式，闪存布局选择原厂，上传

如果你是小米的，先进环境变量山变量，删除这一行

| nomal_firware_md5 | ************ |
| ----------------- | ------------ |



--------------------

## 配置规则

如果你刷成功了，并且到了这一步，恭喜你，距离不远了

路由器重启后，进入OpenWrt,一般网址是192.168.1.1，不知道的可以开cmd看网络配置，输入ipv4地址也可以进，用户名和密码默认是

| root | password |
| ---- | -------- |

----------

## 防检测配置

### NTP服务器

进入 系统设置, 勾选 `Enable NTP client（启用 NTP 客户端）`和 `Provide NTP server`（作为 NTP 服务器提供服务）

NTP server candidates（候选 NTP 服务器）四个框框分别填写 `ntp1.aliyun.com`、`time1.cloud.tencent.com`、`stdtime.gov.hk` 、`pool.ntp.org`

| ntp1.aliyun.com         |
| ----------------------- |
| time1.cloud.tencent.com |
| stdtime.gov.hk          |
| pool.ntp.org            |

-------------

### 防火墙自定义规则

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

-----------

### 使用ssh工具开启ua2f配置

```shell
sudo systemctl status ssh
```



ssh的使用不会的自行学习

打开xshell，主机名就是路由器的ip地址，用户身份验证，就是输入root，和password，如果你刚刚在路由器后台修改了用户名和密码，这里相同

```sql
# 开机自启
uci set ua2f.enabled.enabled=1
# 自动配置防火墙（默认开启）（建议开启）
uci set ua2f.firewall.handle_fw=1
uci set ua2f.firewall.handle_tls=1
uci set ua2f.firewall.handle_mmtls=1
uci set ua2f.firewall.handle_intranet=1
# 保存配置
uci commit ua2f

操作：# 开机自启
service ua2f enable
# 启动ua2f
service ua2f start

# 手动关闭ua2f
service ua2f stop
```

----------------

以上操作完成后，就基本结束了，最后安装上一个克隆mac地址的ipk包，重启后显示，包的链接会放在下方目录。

-------------------------
