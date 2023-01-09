# openEuler 22.03 RISC-V V2版本验收测试报告

修订记录

| 日期       | 修订版本 | 修改章节           | 修改描述   |
| ---------- | -------- | ------------------ | ---------- |
| 2023/1/6 | 1.0.0   | 22.03-V2 |  |
|           |          |          |          |

**摘要**

文本主要描述openEuler 22.03 RISC-V V2版本的整体测试过程，详细叙述测试覆盖情况，并通过问题分析对版本整体质量进行评估和总结。


# 1   概述

openEuler是一款开源操作系统。当前openEuler内核源于Linux，支持RISC-V处理器，能够充分释放计算芯片的潜能，是由全球开源贡献者构建的高效、稳定、安全的开源操作系统。

本文主要描述openEuler 22.03-V2 RISC-V 版本的总体测试活动，按照社区开发模式进行运作，结合社区Tarsier团队制定的版本计划规划相应的测试计划及活动。测试报告覆盖新需求、继承需求的测试执行情况和评估，并结合各类专项测试活动和版本问题单总体情况进行整体的说明和质量评估。

# 2   测试版本说明

本文档测试对象是openEuler 22.03 RISC-V 2022年12月11日和openEuler 22.03-V2 RISC-V（20221228）发布版本，发布范围相较22.03 LTS RISC-V版本主要变动：

1. 软件包选型升级
2. 新增软件：Xfce桌面，Chromium浏览器，Firefox浏览器，Libreoffice办公套件，Tunderbird电子邮件客户端，Eclipse，VLC视频播放工具，GIMP图片编辑工具
3. 新增全栈支持Unmatched开发板，全栈支持VisionFive开发板，部分支持D1开发板
4. 修复bug和cve

测试环境如下：

| 硬件/QEMU | 硬件配置信息 | 测试结果 |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------- |
| HiFive Unmatched | CPU: SiFive Freedom U740 SoC <br />内存：16GB DDR4<br />存储设备：SanDisk Ultra 32GB micro SD | 通过 |
| VisionFive | CPU: JH7100 <br />内存：8GB DDR4<br />存储设备：SanDisk Ultra 32GB micro SD | 通过 |
| D1 | CPU: C906 <br />内存：2GB DDR4<br />存储设备：SanDisk Ultra 32GB micro SD | 基本通过，存在部分缺陷 |
| Qemu 6.2/7.0 | CPU: 8<br />内存：8GB <br />存储设备：文件 | 通过 |

20220926版本测试活动策略如下：

| **需求**                        | **测试分层策略**                                             |
| ------------------------------- | ------------------------------------------------------------ |
| 支持HiFive Unmatched | 对HiFive Unmatched进行安装、基本功能、兼容性及稳定性的测试 |
| 支持VisionFive | 对VisionFive进行安装、基本功能、兼容性及稳定性的测试通过 |
| 支持D1 |启动失败 [启动log](./d1/d1_log.txt) |
| 支持常用软件和系统设置功能软件 | 验证常用软件和系统设置功能软件在openEuler RISC-V版本上的可安装和基本功能 |
| 支持Xfce桌面 | 验证Xfce桌面系统在openEuler RISC-V版本上的可安装和基本功能 |
| 支持Chromium软件 | 验证Chromium软件的安装和软件的基本功能 |
| 支持Firefox软件 | 验证Firefox软件的安装和软件的基本功能 |
| 支持Libreoffice软件 | 验证Libreoffice软件的安装和软件的基本功能 |
| 支持Tunderbird软件 | 验证Tunderbird软件的安装和软件的基本功能 |
| 支持Eclipse软件 | 验证Eclipse软件的安装和软件的基本功能 |
| 支持VLC软件 | 验证VLC软件的安装和软件的基本功能 |
| 支持GIMP软件 | 验证GIMP软件的安装和软件的基本功能 |

openEuler 22.03-V2 RISC-V（20221228）版本测试活动策略如下：

| **需求**                        | **测试分层策略**                                             |
| ------------------------------- | ------------------------------------------------------------ |
| 支持HiFive Unmatched | 对HiFive Unmatched进行安装、基本功能、兼容性及稳定性的测试 |
| 支持VisionFive | 对VisionFive进行安装、基本功能、兼容性及稳定性的测试通过 |
| 支持D1 |对D1进行安装、部分基本功能、兼容性及稳定性的测试通过， 缺陷：WiFi 和蓝牙功能不可用，LibreOffice 启动闪退，修改屏幕分辨率后 xfce 显示可能出现问题，HDMI 接口热插拔可能不可用 |
| 支持常用软件和系统设置功能软件 | 验证常用软件和系统设置功能软件在openEuler RISC-V版本上的可安装和基本功能 |
| 支持Xfce桌面 | 验证Xfce桌面系统在openEuler RISC-V版本上的可安装和基本功能 |
| 支持Chromium软件 | 验证Chromium软件的安装和软件的基本功能 |
| 支持Firefox软件 | 验证Firefox软件的安装和软件的基本功能 |
| 支持Libreoffice软件 | 验证Libreoffice软件的安装和软件的基本功能，D1启动闪退 |
| 支持Tunderbird软件 | 验证Tunderbird软件的安装和软件的基本功能 |
| 支持Eclipse软件 | 验证Eclipse软件的安装和软件的基本功能 |
| 支持VLC软件 | 验证VLC软件的安装和软件的基本功能 |
| 支持GIMP软件 | 验证GIMP软件的安装和软件的基本功能 |

本次版本测试快照构建规则：[ORSP004](https://gitee.com/openeuler/RISC-V/blob/master/proposal/ORSP004.md)

本次版本测试快照责任人：周嘉诚

# 3   Bug分级定义

- P1 / blocking 指阻塞性bug修复之前什么都不能干。例如用户数据丢失可能列为P1

- P2 / important 指用户几乎总会遇到并影响使用，例如常用用例中程序崩溃、关键功能无法使用等

- P3 / normal 指用户经常遇到并且影响使用体验的bug

- P4 / improvement 不紧急的bug

- P5 / wishlist

# 4 测试环境安装

- [x] [使用QEMU安装RISC-V openEuler](./qemu/README.md)

- [x] [使用Unmatched开发板安装RISC-V openEuler](./unmatched/README.md)

- [x] [使用Visionfive开发板安装RISC-V openEuler](./visionfive/README.md)

- [x] [使用D1开发板安装RISC-V openEuler](./d1/README.md)

openEuler 22.03 RISC-V 20220926 QEMU和Unmatched，Visionfive、D1版本通过或基本通过测试发布，

# 5 测试结论

openEuler 22.03 RISC-V 20220926 版本整体测试按照Tarsier团队的计划，共完成了一轮重点特性测试（20220922）+一轮自动化测试（常用软件和系统设置功能）+一轮回归测试+版本发布验收测试（20220926）；其中第一轮测试聚焦在新移植软件的安装和基础功能测试；一轮自动化测试验证交付版本的常用软件和系统设置功能；一轮回归测通过测试第一轮报告的缺陷，验证缺陷的修复和影响程度；版本发布验收测试是在版本正式发布至官网后开展的轻量化验证活动，旨在保证发布件和测试验证过程交付件的一致性。

openEuler 22.03 RISC-V 20220926 版本共发现问题 32个，P1 0 个，P2 1 个，P3 15 个，P4 13 个，P5 3 个，其他问题均已修复，回归测试结果正常。版本整体质量较好。

## 5.1 重点组件测试

对产品所有继承特性进行评价，用表格形式评价，包括特性列表（与特性清单保持一致），验证质量评估，**测试报告见组件名称的链接**。

| 序号 | 组件/特性名称 | 特性质量评估 | 备注 |
| ---- | ----------------------------------------- | :-------------------------: | ---------------------------------------------------------------------------------------------------------------------- |
| 1 | [支持HiFive Unmatched](./unmatched/测试报告.xlsx) | <font color=green>█</font> | 全栈支持Unmatched开发板 |
| 2 | 支持VisionFive | <font color=green>█</font> | 全栈支持VisionFive开发板 |
| 2 | 支持D1 | <font color=green>▲</font> | 部分支持D1开发板, 缺陷：WiFi 和蓝牙功能不可用，LibreOffice 启动闪退，修改屏幕分辨率后 xfce 显示可能出现问题，HDMI 接口热插拔可能不可用 |
| 3 | [支持xfce桌面](./xfce/测试报告.xlsx) | <font color=green>█</font> | 安装和卸载正常，整体核心功能(重要组件和系统插件)稳定正常，整体质量良好，发现缺陷9个。  QEMU和VisionFive屏保锁屏不能解锁（本发行版将卸载屏保程序）, unmatched屏保解锁成功|
| 4 | [支持Chromium浏览器](./chromium/测试报告.xlsx) | <font color=green>█</font> | 安装和卸载正常，整体核心功能(重要组件和系统插件)稳定正常，整体质量良好，发现缺陷2个。 |
| 5 | [支持Firefox浏览器](./firefox/测试报告.xlsx) | <font color=green>█</font> | 安装和卸载正常(此版本源包含97和100两个版本Firefox，安装需使用包全名进行安装，即dnf install firefox-97xxxxx)，整体核心功能(重要组件和系统插件)稳定正常，整体质量良好，发现缺陷8个。 |
| 6 | [支持Libreoffice浏览器](./libreoffice/测试报告.xlsx) | <font color=green>█</font> | 安装正常，卸载失败，整体核心功能(重要组件和系统插件)稳定正常，整体质量良好，发现缺陷2个。 |
| 7 | [支持Tunderbird](./tunderbird/测试报告.xlsx) | <font color=green>█</font> | 安装和卸载正常，整体核心功能(重要组件和系统插件)稳定正常，整体质量良好，可以收发邮件。发现缺陷两例，分别为无法保存邮件内容为样例和无法修改语言为英语外的语言，不影响核心功能使用。 |
| 8 | 支持Eclipse | <font color=green>█</font> | 安装和卸载正常，整体核心功能(重要组件和系统插件)稳定正常，整体质量良好。发现功能缺陷2个，eclipse里面，菜单project下面的open project是灰色的，不能使用，不能打开已有project和eclipse无法配置tomcat。发现性能缺陷1个，软件启动慢，在QEMU和unmatched开发板上的启动时间均超过了5分钟。此测试项目为临时添加，暂未提交测试用例报告。 |
| 9 | [支持VLC](./vlc/测试报告.xlsx) | <font color=blue>▲</font> | 安装和卸载正常，在QEMU和Visionfive无显卡环境下播放mp4视频黑屏，需要手工设置输出格式为X11，unmatched上工作正常，部分设备上播放视频及音频没有声音，未通过测试，从发行版预装软件中删除。发现缺陷5个。 |
| 10 | [支持GIMP](./gimp/测试报告.xlsx) | <font color=green>█</font> | 安装和卸载正常，整体核心功能(重要组件和系统插件)稳定正常，整体质量良好。尚未发现功能缺陷。 |

<font color=red>●</font>： 表示特性不稳定，风险高

<font color=blue>▲</font>： 表示特性基本可用，遗留少量问题

<font color=green>█</font>： 表示特性质量良好

重点软件测试缺陷表
|    软件名称         | P1   | P2         | P3                             | P4                 | P5                         |
| ----------- | ---- | ---------- | ------------------------------ | ------------------ | -------------------------- |
| Firefox     |      |            | 语言设置选项出现乱码             |                    |                            |
|             |      |            | 设置语言后页面无法正常显示        |                    |                            |
|             |      |            | 无法停止下载                    |                    |                            |
|             |      |            | 安装报错                        |                      |                           |
|             |      |            | 下载项显示空白                  |                            |
|             |      |            |                                | 数据不能同步                           |
|             |      |            |                                | 打不开b站          |                            |
|             |      |            |                                | 不能进入阅读模式   |                            |
| VLC         |      |            | 无显卡环境（QEMU, VisionFive），视频播放黑屏，需手工更改视频输出方式X11 |                    |                            |
|             |      |            | 播放卡顿                       |                    |                            |
|             |      |            | 文件标题显示错误               |                    |                            |
|             |      |            | 视频及音频播放无声音             |                 |                              |
|             |      |            |                                | 字幕列表部分显示乱码       |                            |
| GIMP        |      |            |                                |                    | 无法打开使用手册           |
| Thunderbird |      |            |                                |                    | 无法修改语言为英语外的语言 |
|             |      |            |                                | 无法保存邮件内容为样例   |                      |
| Chromuim    |      |            |                                | 谷歌账号数据同步失败   |                            |
|             |      |            |                                |                     | 命令行启动需添加—browser |
| Xfce        |      |自动锁屏无法解锁（QEMU，VisionFive）            |                |                    |                            |
|             |      |            | 应用程序查找器无法查看历史命令 |                    |                            |
|             |      |            | 改伸缩比例                     |                    |                            |
|             |      |            |                                | 回收站没有默认显示 |                            |
|             |      |            |                                | 设置桌面为纯色，无变化     |                            |
|             |      |            |                                | 改变桌面朝向左，无变化     |                            |
|             |      |            |                                | 改变桌面朝向右，无变化     |                            |
|             |      |            |                                | 改变桌面朝向上，无变化     |                            |
|             |      |            |                                | 改变桌面朝向下，无变化     |                            |
| Ecilpse     |      |            | 不能打开已有项目                |                          |                             |
|             |      |            | 无法配置tomcat                  |                          |                            |
|             |      |            |                                | 软件启动时间较长           |                            |
| Libreoffice |      |            | 无法卸载                        |                          |                            |
|             |      |            | 无法验证安装问题                |                           |                            |

在经过修复后生成了openEuler-22.03-V1-riscv64版本，较于20220926版本22.03修复了缺陷P2 1个，P3 1个，删除了P5 1个。

|    软件名称         | P1   | P2         | P3                      | P4                 | P5                         | 备注            |
| ----------- | ---- | ---------- | ------------------------------ | ------------------ | -------------------------- |-------------------------| 
| Firefox            |      |            | 安装报错                |                    |                   | 原先存在97与100两个版本，目前删除了100只保留了97，此缺陷解决 |
| Chromium           |      |            |                        |                    |命令行命令行启动需添加—browser| 站会上决定删除此缺陷       |
| Xfce               |      |自动锁屏无法解锁（QEMU，VisionFive） |              |                     |              | 重新发布了一版删除屏保的镜像，此缺陷解决 |

修复过后openEuler-22.03-V1-riscv64 版本共发现问题 29个，P1 0 个，P2 0 个，P3 13 个，P4 11 个，P5 5 个，以下为22.03-v1版本的重点软件测试缺陷表

|    软件名称  | P1   | P2         | P3                             | P4                 | P5                         |
| ----------- | ---- | ---------- | ------------------------------ | ------------------ | -------------------------- |
| Firefox     |      |            | 语言设置选项出现乱码           |                    |                              |
|             |      |            | 设置语言后页面无法正常显示     |                    |                              |                             
|             |      |            | 无法停止下载                  |                    |                              |                              
|             |      |            | 下载项显示空白                  |                            |                                                
|             |      |            |                                | 数据不能同步                           |                                      
|             |      |            |                                | 打不开b站          |                            |
|             |      |            |                                |                   | 不能进入阅读模式              |
| VLC         |      |            | 无显卡环境（QEMU, VisionFive），视频播放黑屏，需手工更改视频输出方式X11 |                    |                            |
|             |      |            | 播放卡顿                       |                    |                            |
|             |      |            | 文件标题显示错误               |                    |                            |
|             |      |            | 视频及音频播放无声音             |                 |                              |
|             |      |            |                                | 字幕列表部分显示乱码       |                            |
| GIMP        |      |            |                                |                    | 无法打开使用手册           |
| Thunderbird |      |            |                                |                    | 无法修改语言为英语外的语言 |
|             |      |            |                                | 无法保存邮件内容为样例   |                      |
| Chromuim    |      |            |                                |                      | 谷歌账号数据同步失败       |
| Xfce        |      |            |                                |                    | 应用程序查找器无法查看历史命令 |
|             |      |            | 改伸缩比例                     |                    |                            |
|             |      |            |                                | 回收站没有默认显示 |                            |
|             |      |            |                                | 设置桌面为纯色，无变化     |                            |
|             |      |            |                                | 改变桌面朝向左，无变化     |                            |
|             |      |            |                                | 改变桌面朝向右，无变化     |                            |
|             |      |            |                                | 改变桌面朝向上，无变化     |                            |
|             |      |            |                                | 改变桌面朝向下，无变化     |                            |
| Ecilpse     |      |            | 不能打开已有项目                |                          |                             |
|             |      |            | 无法配置tomcat                  |                          |                            |
|             |      |            |                                | 软件启动时间较长           |                            |
| Libreoffice |      |            | 无法卸载                        |                          |                            |
|             |      |            | 无法验证安装问题                |                           |                            |


## 5.2 常见软件和系统功能自动化测试 
- 测试范围：共329个测试套(327个软件包+systemd+os-basic)，1426个测试用例  
- 测试框架：mugen-riscv（由第三测试小队开发维护的mugen分支，新增了测试环境自动复原、多线程测试和测试结果自动分析等功能）   
- 测试方式：测试环境自动复原，测试套间隔离以及自动分配硬盘外设资源的自动化测试  
    使用qemu_test.py，利用qemu qcow2快照实现在测试每个测试套时单独建立qemu虚拟机进行测试，保证了测试套间不会相互干扰。测试程序运行时会根据测试套文件中"add disk"字段的信息，自动创建硬盘资源并分配给对应的虚拟机。    

各测试套测试结果数据统计：  
|序号|测试套|用例总数|通过数|未通过数|
|-----|-------|-----|------|------|
|1|podman|56|0|56|
|2|systemd|160|123|37|
|3|firewalld|22|3|19|
|4|os-basic|101|82|19|
|5|ntfs-3g|24|9|15|
|6|libreswan|15|2|13|
|7|audit|12|0|12|
|8|lxc|13|3|10|
|9|nftables|9|0|9|
|10|rabbitmq-server|11|2|9|
|11|rsyslog|26|17|9|
|12|pcp|39|31|8|
|13|nfs-utils|16|9|7|
|14|openvswitch|7|0|7|
|15|openssh|20|15|5|
|16|dhcp|5|0|5|
|17|open-iscsi|7|2|5|
|18|samba|5|0|5|
|19|glusterfs|5|0|5|
|20|ansible|4|0|4|
|21|clamav|13|9|4|
|22|pcp-system-tools|16|12|4|
|23|targetcli|4|0|4|
|24|iprutils|4|0|4|
|25|bind|4|1|3|
|26|qt5-qttools|12|9|3|
|27|sos|3|0|3|
|28|wireshark|4|1|3|
|29|initscripts|5|2|3|
|30|ipmitool|3|0|3|
|31|lvm2|9|7|2|
|32|osc|8|6|2|
|33|bluez|2|0|2|
|34|chrony|2|0|2|
|35|clevis|4|2|2|
|36|cmake|8|6|2|
|37|cryptsetup|2|0|2|
|38|dejagnu|3|1|2|
|39|linuxptp|2|0|2|
|40|lm_sensors|3|1|2|
|41|mcstrans|2|0|2|
|42|openscap|5|3|2|
|43|procinfo|2|0|2|
|44|psacct|2|0|2|
|45|qemu|3|1|2|
|46|rasdaemon|2|0|2|
|47|rpmdevtools|5|3|2|
|48|sanlock|3|1|2|
|49|security-tool|2|0|2|
|50|strongswan|2|0|2|
|51|freeipmi|3|1|2|
|52|iptables|2|0|2|
|53|freeradius|9|7|2|
|54|ladspa|2|0|2|
|55|java-1.8.0-openjdk|10|8|2|
|56|crontabs|1|0|1|
|57|hostname|1|0|1|
|58|iputils|2|1|1|
|59|kernel|3|2|1|
|60|polkit|1|0|1|
|61|OpenIPMI|1|0|1|
|62|alsa-utils|2|1|1|
|63|anaconda|9|8|1|
|64|arptables|1|0|1|
|65|atune|2|1|1|
|66|auter|1|0|1|
|67|cachefilesd|1|0|1|
|68|conntrack-tools|1|0|1|
|69|container-exception-logger|1|0|1|
|70|corosync|1|0|1|
|71|cups|3|2|1|
|72|dbxtool|1|0|1|
|73|derby|1|0|1|
|74|dnssec-trigger|2|1|1|
|75|docker-engine|1|0|1|
|76|dracut|8|7|1|
|77|easymock|12|11|1|
|78|ebtables|1|0|1|
|79|edac-utils|1|0|1|
|80|fcoe-utils|1|0|1|
|81|lighttpd|1|0|1|
|82|lldpad|2|1|1|
|83|logwatch|1|0|1|
|84|lxcfs|1|0|1|
|85|mailman|1|0|1|
|86|mpg123|1|0|1|
|87|mrtg|1|0|1|
|88|multipath-tools|2|1|1|
|89|mysql|1|0|1|
|90|nagios|1|0|1|
|91|nbdkit|3|2|1|
|92|netlabel_tools|1|0|1|
|93|nss_wrapper|1|0|1|
|94|numad|1|0|1|
|95|nvmetcli|1|0|1|
|96|openmpi|3|2|1|
|97|openvpn|1|0|1|
|98|opensp|6|5|1|
|99|policycoreutils|4|3|1|
|100|pps-tools|1|0|1|
|101|quota|2|1|1|
|102|qperf|1|0|1|
|103|radvd|1|0|1|
|104|rdma-core|2|1|1|
|105|redis|4|3|1|
|106|redis5|4|3|1|
|107|redis6|4|3|1|
|108|rng-tools|1|0|1|
|109|ruby|12|11|1|
|110|rust|8|7|1|
|111|spawn-fcgi|1|0|1|
|112|systemtap|3|2|1|
|113|tuned|1|0|1|
|114|tomcat|3|2|1|
|115|unbound|3|2|1|
|116|vdo|1|0|1|
|117|webbench|1|0|1|
|118|fwupd|2|1|1|
|119|ganglia|2|1|1|
|120|groovy|2|1|1|
|121|iSulad|1|0|1|
|122|iftop|1|0|1|
|123|ipset|1|0|1|
|124|irqbalance|1|0|1|
|125|ipvsadm|1|0|1|
|126|isula-build|1|0|1|
|127|gradle|4|3|1|
|128|keepalived|1|0|1|
|129|kexec-tools|1|0|1|
|130|keyutils|2|1|1|
|131|krb5|3|2|1|
|132|kubernetes|5|4|1|
|133|NetworkManager|4|4|0|
|134|acl|8|8|0|
|135|attr|1|1|0|
|136|cpio|1|1|0|
|137|cracklib|1|1|0|
|138|cronie|2|2|0|
|139|dbus|2|2|0|
|140|dnf|11|11|0|
|141|e2fsprogs|2|2|0|
|142|git|1|1|0|
|143|glibc|2|2|0|
|144|libcap|9|9|0|
|145|man-db|2|2|0|
|146|net-tools|1|1|0|
|147|ntp|4|4|0|
|148|openldap|1|1|0|
|149|openslp|1|1|0|
|150|openssl|28|28|0|
|151|pam|1|1|0|
|152|sqlite|17|17|0|
|153|389-ds-base|2|2|0|
|154|ImageMagick|8|8|0|
|155|ModemManager|1|1|0|
|156|OpenEXR|7|7|0|
|157|PackageKit|2|2|0|
|158|abrt|7|7|0|
|159|accountsservice|1|1|0|
|160|acpid|5|5|0|
|161|amanda|4|4|0|
|162|arpwatch|1|1|0|
|163|at|1|1|0|
|164|authd|1|1|0|
|165|authz|1|1|0|
|166|autoconf213|10|10|0|
|167|avahi|3|3|0|
|168|bcrypt|1|1|0|
|169|bolt|1|1|0|
|170|brltty|1|1|0|
|171|byacc|4|4|0|
|172|ceph|9|9|0|
|173|cgdcbxd|1|1|0|
|174|clang|3|3|0|
|175|cloud-init|6|6|0|
|176|cockpit|3|3|0|
|177|colm|1|1|0|
|178|colord|1|1|0|
|179|cppcheck|2|2|0|
|180|cups-filters|1|1|0|
|181|cvs|2|2|0|
|182|cyrus-sasl|1|1|0|
|183|digest-list-tools|1|1|0|
|184|discount|5|5|0|
|185|djvulibre|3|3|0|
|186|dkms|1|1|0|
|187|dnsmasq|1|1|0|
|188|dos2unix|1|1|0|
|189|dovecot|6|6|0|
|190|doxygen|1|1|0|
|191|erlang|2|2|0|
|192|etcd|6|6|0|
|193|fcgi|1|1|0|
|194|firebird|1|1|0|
|195|timedatex|1|1|0|
|196|util-linux|3|3|0|
|197|wpa_supplicant|1|1|0|
|198|libwbxml|2|2|0|
|199|libzip|3|3|0|
|200|libvma|1|1|0|
|201|memcached|3|3|0|
|202|mlocate|1|1|0|
|203|lsyncd|5|5|0|
|204|lorax|2|2|0|
|205|mariadb|3|3|0|
|206|mosquitto|1|1|0|
|207|mdadm|1|1|0|
|208|mksh|1|1|0|
|209|mt-st|1|1|0|
|210|mutt|1|1|0|
|211|munge|1|1|0|
|212|mysql5|1|1|0|
|213|netcf|1|1|0|
|214|net-snmp|2|2|0|
|215|netdata|1|1|0|
|216|nghttp2|1|1|0|
|217|opensm|1|1|0|
|218|nginx|1|1|0|
|219|nmon|1|1|0|
|220|nodejs|3|3|0|
|221|nss-pam-ldapd|1|1|0|
|222|oddjob|1|1|0|
|223|open-isns|1|1|0|
|224|opencc|1|1|0|
|225|opencryptoki|1|1|0|
|226|openhpi|1|1|0|
|227|optipng|2|2|0|
|228|ostree|1|1|0|
|229|p7zip|5|5|0|
|230|pacemaker|2|2|0|
|231|paps|0|0|0|
|232|pcp-export-pcp2xml|4|4|0|
|233|pcp-export-pcp2json|5|5|0|
|234|pcsc-lite|2|2|0|
|235|perl-Net-Server|1|1|0|
|236|pesign|1|1|0|
|237|php|8|8|0|
|238|plymouth|10|10|0|
|239|pngcrush|5|5|0|
|240|pngquant|1|1|0|
|241|portreserve|1|1|0|
|242|postfix|2|2|0|
|243|powertop|1|1|0|
|244|proftpd|2|2|0|
|245|prometheus2|6|6|0|
|246|rpcbind|2|2|0|
|247|rdate|0|0|0|
|248|realmd|1|1|0|
|249|resource-agents|2|2|0|
|250|rinetd|1|1|0|
|251|smartmontools|1|1|0|
|252|rootsh|0|0|0|
|253|rpmlint|2|2|0|
|254|rrdtool|2|2|0|
|255|rsync|2|2|0|
|256|rtkit|1|1|0|
|257|rubygem-bundler|13|13|0|
|258|sane-backends|1|1|0|
|259|spice-vdagent|2|2|0|
|260|sblim-sfcb|1|1|0|
|261|scsi-target-utils|1|1|0|
|262|switcheroo-control|1|1|0|
|263|sphinx|1|1|0|
|264|sendmail|2|2|0|
|265|squid|1|1|0|
|266|sqlite-jdbc|1|1|0|
|267|storm|4|4|0|
|268|stunnel|1|1|0|
|269|swig|11|11|0|
|270|sssd|17|17|0|
|271|sysprof|2|2|0|
|272|sysstat|3|3|0|
|273|tang|3|3|0|
|274|telnet|1|1|0|
|275|tcllib|3|3|0|
|276|tftp|2|2|0|
|277|udisks2|1|1|0|
|278|tigervnc|1|1|0|
|279|vsftpd|2|2|0|
|280|umoci|1|1|0|
|281|upower|1|1|0|
|282|tidy|16|16|0|
|283|usbmuxd|1|1|0|
|284|uuid|2|2|0|
|285|varnish|2|2|0|
|286|watchdog|3|3|0|
|287|x265|1|1|0|
|288|xfsprogs|1|1|0|
|289|xinetd|1|1|0|
|290|xmltoman|1|1|0|
|291|xdelta|3|3|0|
|292|yelp-tools|3|3|0|
|293|ypbind|1|1|0|
|294|ypserv|3|3|0|
|295|zerofree|1|1|0|
|296|zvbi|1|1|0|
|297|galera|2|2|0|
|298|flatpak|1|1|0|
|299|fprintd|1|1|0|
|300|gpm|1|1|0|
|301|geoclue2|1|1|0|
|302|geos|1|1|0|
|303|gegl04|2|2|0|
|304|gdm|1|1|0|
|305|haproxy|1|1|0|
|306|gnome-shell|1|1|0|
|307|gssproxy|1|1|0|
|308|haveged|1|1|0|
|309|help2man|1|1|0|
|310|hsqldb|1|1|0|
|311|htop|1|1|0|
|312|httpd|4|4|0|
|313|javapackages-tools|6|6|0|
|314|initial-setup|1|1|0|
|315|iperf3|1|1|0|
|316|ipwatchd|1|1|0|
|317|jemalloc|2|2|0|
|318|jq|1|1|0|
|319|jetty|1|1|0|
|320|kf5-kconfig-core|1|1|0|
|321|ksh|1|1|0|
|322|jython|3|3|0|
|323|libcanberra|3|3|0|
|324|libcgroup|1|1|0|
|325|junit5|13|13|0|
|326|libosinfo|3|3|0|
|327|libpng12|1|1|0|
|328|libmemcached|12|12|0|
|329|libstoragemgmt|1|1|0|

未通过测试用例分析：  
|序号|测试套/软件包名|测试用例名|原因|
|------------|---------|----|----|
|1|crontabs|oe_test_crontabs|其他错误|
|2|hostname|oe_test_service_nis-domainname|缺失预装 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|3|iputils|oe_test_service_ninfod|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|4|kernel|oe_test_service_cpupower|缺失预装 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|5|lvm2|oe_test_service_lvmlockd|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|6|lvm2|oe_test_service_lvmlocks|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|7|openssh|oe_test_openssh_port|缺失预装 超时 |
|8|openssh|oe_test_openssh_scp|缺失预装 超时 |
|9|openssh|oe_test_openssh_scp_P|缺失预装 超时 |
|10|openssh|oe_test_openssh_scp_q|缺失预装 超时 |
|11|openssh|oe_test_sec_ssh|文件缺失 |
|12|osc|oe_test_osc_04|其他错误|
|13|osc|oe_test_osc_build|文件缺失 |
|14|polkit|oe_test_service_polkit|systemd单元重启错误 systemd单元运行时错误 |
|15|systemd|oe_test_service_console-getty|缺失预装 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|16|systemd|oe_test_service_dbus-org.freedesktop.import1|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|17|systemd|oe_test_service_dn1|systemd单元重启错误 systemd单元运行时错误 |
|18|systemd|oe_test_service_dbus-org.freedesktop.portable1|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|19|systemd|oe_test_service_initrd-switch-root|缺失预装 systemd单元运行时错误 |
|20|systemd|oe_test_service_quotaon|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|21|systemd|oe_test_service_systemd-ask-password-wall|systemd单元重启错误 systemd单元运行时错误 |
|22|systemd|oe_test_service_systemd-fsck-root|systemd单元运行时错误 |
|23|systemd|oe_test_service_systemd-importd|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|24|systemd|oe_test_service_systemd-initctl|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|25|systemd|oe_test_service_systemd-journal-gatewayd|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|26|systemd|oe_test_service_systemd-journal-remote|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|27|systemd|oe_test_service_systemd-journal-upload|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|28|systemd|oe_test_service_systemd-machined|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|29|systemd|oe_test_service_systemd-network-generator|缺失预装 systemd单元运行时错误 systemd单元使能错误 |
|30|systemd|oe_test_service_systemd-networkd-wait-online|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|31|systemd|oe_test_service_systemd-networkd|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|32|systemd|oe_test_service_systemd-portabled|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|33|systemd|oe_test_service_systemd-quotacheck|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|34|systemd|oe_test_service_systemd-resolved|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|35|systemd|oe_test_service_systemd-sysext|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|36|systemd|oe_test_service_systemd-udevd|systemd单元重启错误 systemd单元运行时错误 |
|37|systemd|oe_test_service_systemd-userdbd|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|38|systemd|oe_test_socket_syslog|缺失预装 |
|39|systemd|oe_test_socket_systemd-journal-gatewayd|文件缺失 |
|40|systemd|oe_test_socket_systemd-journal-remote|缺失软件包 文件缺失 |
|41|systemd|oe_test_socket_systemd-networkd|缺失预装 |
|42|systemd|oe_test_socket_systemd-rfkill|缺失预装 |
|43|systemd|oe_test_socket_systemd-userdbd|缺失预装 |
|44|systemd|oe_test_target_cryptsetup-pre|缺失预装 |
|45|systemd|oe_test_target_cryptsetup|缺失预装 |
|46|systemd|oe_test_target_initrd-switch-root|其他错误|
|47|systemd|oe_test_target_machines|缺失预装 |
|48|systemd|oe_test_target_remote-cryptsetup|缺失预装 |
|49|systemd|oe_test_target_remote-veritysetup|缺失预装 |
|50|systemd|oe_test_target_veritysetup-pre|缺失预装 |
|51|systemd|oe_test_target_veritysetup|缺失预装 |
|52|OpenIPMI|oe_test_service_ipmi|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|53|alsa-utils|oe_test_service_alsa-restore|systemd单元重启错误 systemd单元运行时错误 |
|54|anaconda|oe_test_service_zram|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|55|ansible|oe_test_ansible_01|其他错误|
|56|ansible|oe_test_ansible_02|超时 |
|57|ansible|oe_test_ansible_03|其他错误|
|58|ansible|oe_test_ansible_04|其他错误|
|59|arptables|oe_test_service_arptables|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|60|atune|oe_test_service_atuned|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|61|audit|oe_test_audit_event_log|缺失预装 |
|62|audit|oe_test_audit_fetch_file_in_order|文件缺失 |
|63|audit|oe_test_audit_max_log_file_ignore|缺失预装 |
|64|audit|oe_test_audit_max_log_file_keep_logs|缺失预装 |
|65|audit|oe_test_audit_max_log_file_rotate|缺失预装 |
|66|audit|oe_test_audit_other|缺失预装 |
|67|audit|oe_test_audit_rule_fetch_from_rule|缺失预装 |
|68|audit|oe_test_audit_use_d_audit|缺失预装 |
|69|audit|oe_test_audit_use_w_audit|缺失预装 |
|70|audit|oe_test_audit_user_build_connection|文件缺失 |
|71|audit|oe_test_service_auditd|缺失预装 |
|72|audit|oe_test_start_audit|缺失预装 |
|73|auter|oe_test_auter|其他错误|
|74|bind|oe_test_service_named-chroot-setup|systemd单元重启错误 systemd单元运行时错误 |
|75|bind|oe_test_service_named-chroot|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|76|bind|oe_test_service_named|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|77|bluez|oe_test_service_bluetooth-mesh|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|78|bluez|oe_test_service_bluetooth|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|79|cachefilesd|oe_test_service_cachefilesd|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|80|chrony|oe_test_service_chrony-wait|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|81|chrony|oe_test_service_chronyd|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|82|clamav|oe_test_clamav_clamonacc|文件缺失 超时 |
|83|clamav|oe_test_clamav_clamscan_2|文件缺失 超时 |
|84|clamav|oe_test_clamav_clamsubmit|文件缺失 |
|85|clamav|oe_test_service_clamav-clamonacc|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|86|clevis|oe_test_install_clevis|文件缺失 |
|87|clevis|oe_test_service_clevis-luks-askpass|systemd单元运行时错误 |
|88|cmake|oe_test_ccmake|超时 |
|89|cmake|oe_test_ccmake3|超时 |
|90|conntrack-tools|oe_test_service_conntrackd|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|91|container-exception-logger|oe_test_container-exception-logger|文件缺失 |
|92|corosync|oe_test_service_spausedd|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|93|cryptsetup|oe_test_encrypt_data|文件缺失 |
|94|cryptsetup|oe_test_luks_encrypted|文件缺失 超时 |
|95|cups|oe_test_socket_cups-lpd|文件缺失 |
|96|dbxtool|oe_test_service_dbxtool|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|97|dejagnu|oe_test_dejagnu_runtest_01|文件缺失 |
|98|dejagnu|oe_test_dejagnu_runtest_02|其他错误|
|99|derby|oe_test_service_derby|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|100|dhcp|oe_test_allocate_ipv4_addresses_dhcpd|文件缺失 |
|101|dhcp|oe_test_allocate_ipv6_addresses_dhcpd|文件缺失 |
|102|dhcp|oe_test_service_dhcpd|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|103|dhcp|oe_test_service_dhcpd6|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|104|dhcp|oe_test_service_dhcrelay|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|105|dnssec-trigger|oe_test_service_dnssec-triggerd|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|106|docker-engine|oe_test_service_docker|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|107|dracut|oe_test_service_dracut-shutdown|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|108|easymock|oe_test_easymock_spring|缺失软件包 |
|109|ebtables|oe_test_service_ebtables|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|110|edac-utils|oe_test_service_edac|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|111|fcoe-utils|oe_test_service_fcoe|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|112|firewalld|oe_test_firewalld_add_sourceip|缺失预装 |
|113|firewalld|oe_test_firewalld_add_sourceport|缺失预装 |
|114|firewalld|oe_test_firewalld_getzone|缺失预装 |
|115|firewalld|oe_test_firewalld_ip_camouflage|缺失预装 |
|116|firewalld|oe_test_firewalld_list|缺失预装 |
|117|firewalld|oe_test_firewalld_lockdown|缺失预装 |
|118|firewalld|oe_test_firewalld_log_denied|文件缺失 超时 |
|119|firewalld|oe_test_firewalld_new_zone|缺失预装 |
|120|firewalld|oe_test_firewalld_runtime_permanent|缺失预装 |
|121|firewalld|oe_test_firewalld_set_target|缺失预装 |
|122|firewalld|oe_test_firewalld_start_check|缺失预装 |
|123|firewalld|oe_test_firewalld_start_status|缺失预装 |
|124|firewalld|oe_test_firewalld_start_stop|缺失预装 |
|125|firewalld|oe_test_firewalld_whitelist_command|缺失预装 |
|126|firewalld|oe_test_firewalld_whitelist_contexts|缺失预装 |
|127|firewalld|oe_test_firewalld_whitelist_uids|缺失预装 |
|128|firewalld|oe_test_firewalld_whitelist_user|缺失预装 |
|129|firewalld|oe_test_firewalld_zone_add_service|缺失预装 |
|130|firewalld|oe_test_service_firewalld|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|131|lighttpd|oe_test_service_lighttpd|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|132|linuxptp|oe_test_service_ptp4l|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|133|linuxptp|oe_test_service_phc2sys|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|134|lldpad|oe_test_service_lldpad|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|135|lm_sensors|oe_test_service_fancontrol|用例执行错误 缺失内核模块 |
|136|lm_sensors|oe_test_service_lm_sensors|用例执行错误 缺失内核模块 |
|137|logwatch|oe_test_logwatch|文件缺失 超时 |
|138|lxcfs|oe_test_service_lxcfs|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|139|mailman|oe_test_service_mailman|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|140|mcstrans|oe_test_service_mcstrans|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|141|mcstrans|oe_test_service_mcstransd|systemd单元重启错误 systemd单元运行时错误 |
|142|lxc|oe_test_lxc_ls_monitor|文件缺失 |
|143|lxc|oe_test_lxc_create_attach|文件缺失 |
|144|lxc|oe_test_lxc_unfreeze_destroy|文件缺失 |
|145|lxc|oe_test_lxc_snapshot_start|文件缺失 |
|146|lxc|oe_test_lxc_info|文件缺失 |
|147|lxc|oe_test_lxc_unshare_update|文件缺失 超时 |
|148|lxc|oe_test_lxc_stop_top|文件缺失 超时 |
|149|lxc|oe_test_lxc_autostart_cgroup|文件缺失 |
|150|lxc|oe_test_lxc_device_copy|文件缺失 |
|151|lxc|oe_test_service_lxc-net|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|152|mpg123|oe_test_mpg123|其他错误|
|153|mrtg|oe_test_service_mrtg|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|154|multipath-tools|oe_test_service_multipathd|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|155|mysql|oe_test_service_mysql|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|156|nagios|oe_test_service_nagios|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|157|nftables|oe_test_nftables_backup_rules|缺失预装 |
|158|nftables|oe_test_nftables_chains|缺失预装 |
|159|nftables|oe_test_iptables_to_nftables|其他错误|
|160|nftables|oe_test_nftables_create_counters|文件缺失 |
|161|nftables|oe_test_nftables_name_sets|缺失预装 |
|162|nftables|oe_test_service_nftables|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|163|nftables|oe_test_nftables_listen_package|缺失预装 超时 |
|164|nftables|oe_test_nftables_replace_counters|缺失预装 |
|165|nftables|oe_test_nftables_anonymous_map|缺失预装 |
|166|nbdkit|oe_test_nbdkit_02|无效参数 |
|167|netlabel_tools|oe_test_service_netlabel|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|168|nss_wrapper|oe_test_nss_wrapper|其他错误|
|169|numad|oe_test_service_numad|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|170|nvmetcli|oe_test_service_nvmet|缺失内核模块 文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|171|nfs-utils|oe_test_service_nfs|systemd单元重启错误 systemd单元运行时错误 |
|172|nfs-utils|oe_test_service_nfsdcld|systemd单元重启错误 systemd单元运行时错误 |
|173|nfs-utils|oe_test_service_nfs-idmapd|systemd单元重启错误 systemd单元运行时错误 |
|174|nfs-utils|oe_test_service_nfs-idmap|systemd单元重启错误 systemd单元运行时错误 |
|175|nfs-utils|oe_test_service_nfs-mountd|systemd单元重启错误 systemd单元运行时错误 |
|176|nfs-utils|oe_test_service_nfs-server|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|177|nfs-utils|oe_test_service_nfs-blkmap|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 无效参数 |
|178|open-iscsi|oe_test_socket_iscsiuio|文件缺失 |
|179|open-iscsi|oe_test_open-iscsi_iscsistart_iscsiuio|用例执行错误 文件缺失 超时 |
|180|open-iscsi|oe_test_service_iscsiuio|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|181|open-iscsi|oe_test_open-iscsi_iscsiadm|用例执行错误 文件缺失 超时 |
|182|open-iscsi|oe_test_service_iscsid|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|183|openmpi|oe_test_openmpi_cluster|用例执行错误 超时 |
|184|ntfs-3g|oe_test_ntfs-3g_lowntfs-3g_02|其他错误|
|185|ntfs-3g|oe_test_ntfs-3g_ntfsinfo|文件缺失 |
|186|ntfs-3g|oe_test_ntfs-3g_ntfsls|其他错误|
|187|ntfs-3g|oe_test_ntfs-3g_ntfsfallocate|文件缺失 |
|188|ntfs-3g|oe_test_ntfs-3g_ntfsundelete_02|其他错误|
|189|ntfs-3g|oe_test_ntfs-3g_ntfssecaudit|其他错误|
|190|ntfs-3g|oe_test_ntfs-3g_ntfsundelete_01|其他错误|
|191|ntfs-3g|oe_test_ntfs-3g_lowntfs-3g_03|其他错误|
|192|ntfs-3g|oe_test_ntfs-3g_ntfs-3g_02|其他错误|
|193|ntfs-3g|oe_test_ntfs-3g_ntfscp|其他错误|
|194|ntfs-3g|oe_test_ntfs-3g_ntfsmove|其他错误|
|195|ntfs-3g|oe_test_ntfs-3g_ntfscluster|其他错误|
|196|ntfs-3g|oe_test_ntfs-3g_lowntfs-3g_01|其他错误|
|197|ntfs-3g|oe_test_ntfs-3g_ntfs-3g_03|其他错误|
|198|ntfs-3g|oe_test_ntfs-3g_ntfs-3g_01|其他错误|
|199|openvpn|oe_test_openvpn|超时 |
|200|openvswitch|oe_test_service_ovn-northd|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|201|openvswitch|oe_test_service_ovs-vswitchd|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|202|openvswitch|oe_test_service_openvswitch|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|203|openvswitch|oe_test_service_openvswitch-ipsec|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|204|openvswitch|oe_test_service_ovn-controller-vtep|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|205|openvswitch|oe_test_service_ovsdb-server|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|206|openvswitch|oe_test_service_ovn-controller|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|207|openscap|oe_test_scanning_remote_system|文件缺失 超时 |
|208|openscap|oe_test_assess_safety_compliance|文件缺失 超时 |
|209|opensp|oe_test_opensp_osgmlnorm|超时 |
|210|pcp-system-tools|oe_test_pcp-iostat|其他错误|
|211|pcp-system-tools|oe_test_pcp-mpstat_pcp-numastat|其他错误|
|212|pcp-system-tools|oe_test_dstat_03|文件缺失 |
|213|pcp-system-tools|oe_test_pcp-pidstat_02_pcp-ipcs|其他错误|
|214|policycoreutils|oe_test_service_restorecond|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|215|pcp|oe_test_pmlogger_daily_01|其他错误|
|216|pcp|oe_test_pmval_02|文件缺失 |
|217|pcp|oe_test_pmevent_02|文件缺失 |
|218|pcp|oe_test_service_pmmgr|缺失软件包 文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|219|pcp|oe_test_pmhostname_pmlock_pmlogger_check|其他错误|
|220|pcp|oe_test_pmlogger_daily_report|文件缺失 |
|221|pcp|oe_test_service_pmwebd|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|222|pcp|oe_test_pmprobe_01|文件缺失 |
|223|pps-tools|oe_test_pps-tools|文件缺失 无效参数 |
|224|quota|oe_test_service_quota_nld|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|225|procinfo|oe_test_procinfo_01|其他错误|
|226|procinfo|oe_test_procinfo_02|无效参数 |
|227|psacct|oe_test_psacct|其他错误|
|228|psacct|oe_test_service_psacct|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|229|qperf|oe_test_qperf_01|超时 |
|230|qemu|oe_test_service_qemu-pr-helper|systemd单元重启错误 systemd单元运行时错误 |
|231|qemu|oe_test_service_qemu-guest-agent|systemd单元重启错误 systemd单元运行时错误 |
|232|podman|oe_test_podman_DK_07|超时 |
|233|podman|oe_test_podman_18|其他错误|
|234|podman|oe_test_podman_28|其他错误|
|235|podman|oe_test_podman_DK_03|文件缺失 |
|236|podman|oe_test_podman_DK_18|其他错误|
|237|podman|oe_test_podman_01|文件缺失 |
|238|podman|oe_test_podman_DK_19|其他错误|
|239|podman|oe_test_podman_07|超时 |
|240|podman|oe_test_podman_04|文件缺失 |
|241|podman|oe_test_podman_DK_02|其他错误|
|242|podman|oe_test_podman_27|其他错误|
|243|podman|oe_test_podman_DK_11|其他错误|
|244|podman|oe_test_podman_06|文件缺失 |
|245|podman|oe_test_podman_10|其他错误|
|246|podman|oe_test_socket_io.podman|文件缺失 |
|247|podman|oe_test_podman_03|文件缺失 |
|248|podman|oe_test_podman_DK_15|文件缺失 超时 |
|249|podman|oe_test_podman_DK_20|其他错误|
|250|podman|oe_test_podman_DK_01|文件缺失 |
|251|podman|oe_test_podman_DK_26|其他错误|
|252|podman|oe_test_podman_DK_14|其他错误|
|253|podman|oe_test_podman_DK_13|其他错误|
|254|podman|oe_test_podman_02|其他错误|
|255|podman|oe_test_podman_DK_25|其他错误|
|256|podman|oe_test_podman_11|其他错误|
|257|podman|oe_test_podman_14|其他错误|
|258|podman|oe_test_podman_22|其他错误|
|259|podman|oe_test_service_io.podman|文件缺失 systemd单元运行时错误 |
|260|podman|oe_test_podman_DK_08|文件缺失 |
|261|podman|oe_test_podman_DK_10|其他错误|
|262|podman|oe_test_podman_16|文件缺失 |
|263|podman|oe_test_podman_12|其他错误|
|264|podman|oe_test_podman_05|文件缺失 |
|265|podman|oe_test_podman_DK_05|文件缺失 |
|266|podman|oe_test_podman_13|其他错误|
|267|podman|oe_test_podman_DK_17|其他错误|
|268|podman|oe_test_podman_DK_23|其他错误|
|269|podman|oe_test_podman_19|其他错误|
|270|podman|oe_test_podman_DK_28|其他错误|
|271|podman|oe_test_podman_23|其他错误|
|272|podman|oe_test_podman_20|其他错误|
|273|podman|oe_test_podman_08|文件缺失 |
|274|podman|oe_test_podman_DK_16|文件缺失 |
|275|podman|oe_test_podman_15|文件缺失 超时 |
|276|podman|oe_test_podman_DK_04|文件缺失 |
|277|podman|oe_test_podman_DK_12|其他错误|
|278|podman|oe_test_podman_DK_22|其他错误|
|279|podman|oe_test_podman_24|其他错误|
|280|podman|oe_test_podman_17|其他错误|
|281|podman|oe_test_podman_DK_27|其他错误|
|282|podman|oe_test_podman_25|其他错误|
|283|podman|oe_test_podman_DK_06|文件缺失 |
|284|podman|oe_test_podman_26|其他错误|
|285|podman|oe_test_podman_21|其他错误|
|286|podman|oe_test_podman_DK_24|其他错误|
|287|podman|oe_test_podman_DK_21|其他错误|
|288|qt5-qttools|oe_test_qt5-qttools_qdoc_02|其他错误|
|289|qt5-qttools|oe_test_qt5-qttools_qdoc_03|其他错误|
|290|qt5-qttools|oe_test_qt5-qttools_qdbus-qt5|其他错误|
|291|radvd|oe_test_service_radvd|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|292|rasdaemon|oe_test_service_ras-mc-ctl|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|293|rasdaemon|oe_test_service_rasdaemon|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|294|rdma-core|oe_test_socket_ibacm|文件缺失 |
|295|redis|oe_test_redis_02|超时 |
|296|redis5|oe_test_redis5_02|超时 |
|297|redis6|oe_test_redis6_02|超时 |
|298|rng-tools|oe_test_service_rngd|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|299|rabbitmq-server|oe_test_rabbitmq-plugins|其他错误|
|300|rabbitmq-server|oe_test_rabbitmqctl_user|其他错误|
|301|rabbitmq-server|oe_test_service_rabbitmq-server|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|302|rabbitmq-server|oe_test_rabbitmqctl_policy|其他错误|
|303|rabbitmq-server|oe_test_rabbitmqctl_access|其他错误|
|304|rabbitmq-server|oe_test_rabbitmqctl_parameter|其他错误|
|305|rabbitmq-server|oe_test_rabbitmqctl_app|其他错误|
|306|rabbitmq-server|oe_test_rabbitmq-plugins_list|超时 |
|307|rabbitmq-server|oe_test_rabbitmqctl_status|其他错误|
|308|rpmdevtools|oe_test_rpmdevtools_rpmargs|超时 |
|309|rpmdevtools|oe_test_rpmdevtools_rpmdev-wipetree|用例执行错误 超时 |
|310|ruby|oe_test_irb_01|其他错误|
|311|rsyslog|oe_test_rsyslog_reliability_tcp|文件缺失 超时 |
|312|rsyslog|oe_test_rsyslog_abnormal_template|超时 |
|313|rsyslog|oe_test_rsyslog_function_tcp|文件缺失 超时 |
|314|rsyslog|oe_test_rsyslog_function_attribute|文件缺失 超时 |
|315|rsyslog|oe_test_rsyslog_function_udp|文件缺失 超时 |
|316|rsyslog|oe_test_rsyslog_function_relp|文件缺失 超时 |
|317|rsyslog|oe_test_rsyslog_function_tcp_firewall|文件缺失 超时 |
|318|rsyslog|oe_test_rsyslog_function_httpd|超时 |
|319|rsyslog|oe_test_rsyslog_reliability_lenght|文件缺失 超时 |
|320|rust|oe_test_cargo_02|其他错误|
|321|samba|oe_test_service_smb|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|322|samba|oe_test_service_nmb|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|323|samba|oe_test_service_winbind|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|324|samba|oe_test_service_samba|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|325|samba|oe_test_service_ctdb|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|326|sanlock|oe_test_service_wdmd|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|327|sanlock|oe_test_service_sanlk-resetd|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|328|security-tool|oe_test_security_tool|文件缺失 |
|329|security-tool|oe_test_service_openEuler-security|缺失预装 systemd单元运行时错误 systemd单元使能错误 |
|330|spawn-fcgi|oe_test_service_spawn-fcgi|systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|331|strongswan|oe_test_service_strongswan-swanctl|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|332|strongswan|oe_test_service_strongswan|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|333|sos|oe_test_sosreport_02|超时 |
|334|sos|oe_test_sosreport_04|其他错误|
|335|sos|oe_test_sosreport_03|文件缺失 |
|336|systemtap|oe_test_service_systemtap|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|337|targetcli|oe_test_targetcli_02|其他错误|
|338|targetcli|oe_test_targetcli_04|文件缺失 |
|339|targetcli|oe_test_targetcli_03|文件缺失 |
|340|targetcli|oe_test_targetcli_01|其他错误|
|341|tuned|oe_test_service_tuned|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|342|tomcat|oe_test_service_tomcat-jsvc|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|343|unbound|oe_test_service_unbound-keygen|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|344|vdo|oe_test_service_vdo|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|345|webbench|oe_test_webbench|其他错误|
|346|os-basic|oe_test_kernel_module_operation|缺失内核模块 |
|347|os-basic|oe_test_awk|其他错误|
|348|os-basic|oe_test_disk_schedule_specific|无效参数 |
|349|os-basic|oe_test_server_httpd_restart|其他错误|
|350|os-basic|oe_test_disk_graphics_card|文件缺失 |
|351|os-basic|oe_test_server_squid_blacklist|其他错误|
|352|os-basic|oe_test_who|其他错误|
|353|os-basic|oe_test_server_squid_proxy|文件缺失 |
|354|os-basic|oe_test_nmcli_set_bond|缺失预装 |
|355|os-basic|oe_test_power_powertop2tuned_optimize|其他错误|
|356|os-basic|oe_test_nmcli_set_team|其他错误|
|357|os-basic|oe_test_server_openssh_secure|其他错误|
|358|os-basic|oe_test_server_openssh_verifykey|文件缺失 超时 |
|359|os-basic|oe_test_server_httpd_checkfirewall|其他错误|
|360|os-basic|oe_test_kernel_kdump|缺失预装 |
|361|os-basic|oe_test_disk_schedule_udev|缺失预装 |
|362|os-basic|oe_test_server_squid_ip|其他错误|
|363|os-basic|oe_test_server_httpd_tls|其他错误|
|364|os-basic|oe_test_system_monitor_share_total|其他错误|
|365|wireshark|oe_test_captype|文件缺失 |
|366|wireshark|oe_test_tshark_03|超时 |
|367|wireshark|oe_test_randpkt-reordercap|文件缺失 |
|368|freeipmi|oe_test_service_bmc-watchdog|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|369|freeipmi|oe_test_service_ipmiseld|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|370|fwupd|oe_test_service_fwupd|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|371|ganglia|oe_test_service_gmetad|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|372|glusterfs|oe_test_service_glusterfsd|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|373|glusterfs|oe_test_service_glusterd|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|374|glusterfs|oe_test_service_glusterfssharedstorage|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|375|glusterfs|oe_test_service_gluster-ta-volume|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|376|glusterfs|oe_test_service_glustereventsd|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|377|groovy|oe_test_groovy_02|文件缺失 |
|378|iSulad|oe_test_service_isulad|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|379|iftop|oe_test_iftop_gui|文件缺失 |
|380|initscripts|oe_test_service_loadmodules|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|381|initscripts|oe_test_service_netconsole|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|382|initscripts|oe_test_service_import-state|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|383|iprutils|oe_test_service_iprinit|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|384|iprutils|oe_test_service_iprdump|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|385|iprutils|oe_test_service_iprupdate|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|386|iprutils|oe_test_target_iprutils|缺失预装 |
|387|ipmitool|oe_test_service_ipmievd|缺失内核模块 文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|388|ipmitool|oe_test_service_bmc-snmp-proxy|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|389|ipmitool|oe_test_service_exchange-bmc-os-info|文件缺失 systemd单元重启错误 systemd单元运行时错误 |
|390|ipset|oe_test_service_ipset|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|391|iptables|oe_test_service_ip6tables|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|392|iptables|oe_test_service_iptables|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|393|irqbalance|oe_test_service_irqbalance|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|394|ipvsadm|oe_test_service_ipvsadm|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|395|freeradius|oe_test_freeradius_freeradius-utils_radclient2|其他错误|
|396|freeradius|oe_test_freeradius_freeradius-utils_radeapclient|超时 |
|397|isula-build|oe_test_service_isula-build|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|398|gradle|oe_test_gradle_04|其他错误|
|399|keepalived|oe_test_service_keepalived|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|400|kexec-tools|oe_test_service_kdump|缺失预装 systemd单元重启错误 systemd单元运行时错误 |
|401|keyutils|oe_test_keyutils-api|文件缺失 |
|402|krb5|oe_test_service_kadmin|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 无效参数 |
|403|ladspa|oe_test_ladspa_analyseplugin|其他错误|
|404|ladspa|oe_test_ladspa_applyplugin|其他错误|
|405|java-1.8.0-openjdk|oe_test_openjdk_appletviewer_clhsdb|其他错误|
|406|java-1.8.0-openjdk|oe_test_openjdk_jdb_jdeps|文件缺失 |
|407|libreswan|oe_test_libreswan_ipsec_check|文件缺失 |
|408|libreswan|oe_test_libreswan_ipsec_whack_1|其他错误|
|409|libreswan|oe_test_libreswan_ipsec_02|文件缺失 |
|410|libreswan|oe_test_service_ipsec|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |
|411|libreswan|oe_test_host_to_host_vpn|文件缺失 超时 |
|412|libreswan|oe_test_libreswan_ipsec_01|其他错误|
|413|libreswan|oe_test_libreswan_ipsec_whack_2|其他错误|
|414|libreswan|oe_test_libreswan_ipsec_setup|超时 |
|415|libreswan|oe_test_libreswan_ipsec_systemctl|超时 |
|416|libreswan|oe_test_libreswan_ipsec_whack_3|其他错误|
|417|libreswan|oe_test_libreswan_ipsec_03|其他错误|
|418|libreswan|oe_test_libreswan_ipsec_whack_4|其他错误|
|419|libreswan|oe_test_site_to_site_vpn|文件缺失 超时 |
|420|kubernetes|oe_test_service_kube-proxy|文件缺失 systemd单元重启错误 systemd单元运行时错误 systemd单元使能错误 |


# 6 用户反馈开发需求

| **序号** | **特性名称** | 等级 |
| -------- | ---------------------------- | ------------------------------------------------------------ |
| 1 | 镜像预装中文输入法                                           | P3 |
| 2 |eclipse支持tomcat插件的安装与配置| P4 |

# 7. 附件

1. [RISC-V openEuler 22.03 12月11号测试镜像自动化测试报告](./auto_testing/1211-22.03testing)
2. [RISC-V openEuler 22.03 preview V2 自动化测试报告](./auto_testing/openEuler-RISC-V-22.03-Preview-V2)
3. [RISC-V openEuler 22.03-0926版本测试说明](https://github.com/FIFCC/plct-testing/blob/main/20220926v0.2/README.md)
4. [RISC-V openEuler 22.03-v1版本测试说明](https://github.com/FIFCC/plct-testing/blob/main/22.03-v1/README.md)
