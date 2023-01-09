## 使用D1 开发板安装openEuler RISC-V 镜像

以下为20220926版本安装文档（启动失败），V1版本（启动成功）安装文档见https://gitee.com/openeuler/RISC-V/blob/master/release/openEuler-22.03/d1/README.md

### 1. 准备硬件

1）D1开发板：由D1获取得到开发板。

2）64G micro-sd卡及读卡器：SanDisk TF/MicroSD卡，容量64GB，速度U1，带读卡器。

3）Usb转uart串口通信模块：丢石头 PL2303，3.3/5V电平输出，type A接口，10PIN散头杜邦线。

4）电源适配器及type-c线。

5）连接D1开发板的3-Pin DEBUG端和Usb转uart串口通信模块。

照片：

![figure_3](./images/figure_3.jpg)

### 2. 准备系统镜像

D1的系统镜像下载连接地址如下： https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/testing/20220926/v0.1/D1/

考虑到要安装验证Firefox浏览器，我们可以下载openeuler-d1-xfce.img.tar.zst，连接如下： https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/testing/20220926/v0.1/D1/openeuler-d1-xfce.img.tar.zst

其他文件均无需下载。

```bash
wget https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/testing/20220926/v0.1/D1/openeuler-d1-xfce.img.tar.zst 
```

### 3. 刷写镜像

以下步骤适用于Ubuntu20.04，如适用Windows操作系统，解压请下载[zstd](./zstd-v1.4.4-win32.zip)`zstd.exe -d ./openeuler-d1-xfce.img.tar.zst`，之后将.img.tar解压为.img文件，刷写请下载[win32diskimager](https://sourceforge.net/projects/win32diskimager/)

1. 解压镜像文件

```bash
sudo apt install zstd -y
tar -I zstdmt -xvf ./openeuler-d1.img.tar.zst
```

2. 镜像刷写

将64G micro-sd卡装入读卡器后，插入笔记本电脑。笔记本电脑通常带一个硬盘，所以sd卡对应设备是/dev/sdb

```bash
sudo dd if=./openeuler-d1-xfce.img of=/dev/sdb bs=1M iflag=fullblock oflag=direct conv=fsync status=progress
```

### 4. 安装串口调试软件

1）将Usb转uart串口通信模块连接到电脑usb口。

2）检查设备管理器中的COM端口，例如COM4。

![figure_2](./images/figure_2.png)

3）使用Xmodem安装固件。

安装teraterm，https://mobaxterm.mobatek.net/download.html

    选择菜单setup->Serial port setup
    Speed设置为115200
    Data设置为8bit
    Paritv设置为none
    Stoo bits设置为1bit
    Flowcontrol设置为none

![figure_4](./images/figure_4.png)

### 5. 启动D1

启动失败，Starting kernel ...显示后系统挂起。

```
[37]HELLO! BOOT0 is starting!
[40]BOOT0 commit :
[42]set pll start
[44]periph0 has been enabled
[46]set pll end
[48]board init ok
[50]DRAM only have internal ZQ!!
[53]get_pmu_exist() = -1
[55]ddr_efuse_type: 0x0
[58][AUTO DEBUG] two rank and full DQ!
[62]ddr_efuse_type: 0x0
[65][AUTO DEBUG] rank 0 row = 15
[68][AUTO DEBUG] rank 0 bank = 8
[71][AUTO DEBUG] rank 0 page size = 2 KB
[75][AUTO DEBUG] rank 1 row = 15
[78][AUTO DEBUG] rank 1 bank = 8
[81][AUTO DEBUG] rank 1 page size = 2 KB
[85]rank1 config same as rank0
[88]DRAM BOOT DRIVE INFO: V0.24
[91]DRAM CLK = 792 MHz
[93]DRAM Type = 3 (2:DDR2,3:DDR3)
[96]DRAMC ZQ value: 0x7b7bfb
[98]DRAM ODT value: 0x42.
[101]ddr_efuse_type: 0x0
[104]DRAM SIZE =1024 M
[108]DRAM simple test OK.
[110]dram size =1024
[112]card no is 0
[114]sdcard 0 line count 4
[116][mmc]: mmc driver ver 2021-04-2 16:45
[125][mmc]: Wrong media type 0x0
[128][mmc]: ***Try SD card 0***
[147][mmc]: HSSDR52/SDR25 4 bit
[150][mmc]: 50000000 Hz
[152][mmc]: 30436 MB
[154][mmc]: ***SD/MMC 0 init OK!!!***
[192]Loading boot-pkg Succeed(index=1).
[196]Entry_name        = opensbi
[199]Entry_name        = dtb
[202]Entry_name        = u-boot
[205]Adding DRAM info to DTB.
[209]Jump to second Boot.

OpenSBI v0.9
   ____                    _____ ____ _____
  / __ \                  / ____|  _ \_   _|
 | |  | |_ __   ___ _ __ | (___ | |_) || |
 | |  | | '_ \ / _ \ '_ \ \___ \|  _ < | |
 | |__| | |_) |  __/ | | |____) | |_) || |_
  \____/| .__/ \___|_| |_|_____/|____/_____|
        | |
        |_|

Platform Name             : Allwinner D1 NeZha
Platform Features         : medeleg
Platform HART Count       : 1
Platform IPI Device       : aclint-mswi
Platform Timer Device     : aclint-mtimer @ 24000000Hz
Platform Console Device   : uart8250
Platform HSM Device       : ---
Platform Reboot Device    : sunxi-wdt-reset
Platform Shutdown Device  : ---
Firmware Base             : 0x40000000
Firmware Size             : 248 KB
Runtime SBI Version       : 0.3

Domain0 Name              : root
Domain0 Boot HART         : 0
Domain0 HARTs             : 0*
Domain0 Region00          : 0x0000000014008000-0x000000001400bfff (I)
Domain0 Region01          : 0x0000000014000000-0x0000000014007fff (I)
Domain0 Region02          : 0x0000000040000000-0x000000004003ffff ()
Domain0 Region03          : 0x0000000000000000-0xffffffffffffffff (R,W,X)
Domain0 Next Address      : 0x000000004a000000
Domain0 Next Arg1         : 0x0000000044000000
Domain0 Next Mode         : S-mode
Domain0 SysReset          : yes

Boot HART ID              : 0
Boot HART Domain          : root
Boot HART ISA             : rv64imafdcvsux
Boot HART Features        : scounteren,mcounteren,mcountinhibit,time
Boot HART PMP Count       : 16
Boot HART PMP Granularity : 2048
Boot HART PMP Address Bits: 38
Boot HART MHPM Count      : 0
Boot HART MIDELEG         : 0x0000000000000222
Boot HART MEDELEG         : 0x000000000000b109


U-Boot 2021.10 (May 20 2022 - 11:19:07 +0800)

DRAM:  1 GiB
WDT:   Started watchdog@6011000 with servicing (16s timeout)
MMC:   mmc@4020000: 0, mmc@4021000: 1
Loading Environment from nowhere... OK
In:    serial@2500000
Out:   serial@2500000
Err:   serial@2500000
Net:
Warning: ethernet@4500000 (eth0) using random MAC address - ea:d0:77:87:b3:58
eth0: ethernet@4500000
Hit any key to stop autoboot:  0
switch to partitions #0, OK
mmc0 is current device
Scanning mmc 0:2...
Found /extlinux/extlinux.conf
Retrieving file: /extlinux/extlinux.conf
364 bytes read in 2 ms (177.7 KiB/s)
1:      Linux openEuler-riscv
Retrieving file: /Image
17629036 bytes read in 3034 ms (5.5 MiB/s)
append: earlyprintk rw root=/dev/mmcblk0p3 rootfstype=ext4 rootwait console=ttyS0,115200 earlycon
Retrieving file: /sun20i-d1-nezha.dtb
24602 bytes read in 6 ms (3.9 MiB/s)
## Flattened Device Tree blob at 4fa00000
   Booting using the fdt blob at 0x4fa00000
   Loading Device Tree to 0000000049ff6000, end 0000000049fff019 ... OK

Starting kernel ...

```
