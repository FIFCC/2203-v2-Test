# RISC-V oE 2022-12-11 22.03测试镜像 mugen自动化测试结果说明  
## 测试说明  
### 测试范围   
- 共333个测试套(331个软件包+systemd+os-basic)，1582个测试用例  
### 测试框架和测试方法  
- 测试框架：mugen-riscv   
- 测试方式：测试环境自动复原，测试套间隔离以及自动分配硬盘外设资源的自动化测试  
    使用qemu_test.py，利用qemu qcow2快照实现在测试每个测试套时单独建立qemu虚拟机进行测试，保证了测试套间不会相互干扰。测试程序运行时会根据测试套文件中"add disk"字段的信息，自动创建硬盘资源并分配给对应的虚拟机。  
- 测试用例代码位置：https://github.com/brsf11/mugen-riscv/tree/riscv/testcases/cli-test/对应测试套名/对应测试用例名.sh  

### 测试环境  
- 本次测试使用镜像：https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/testing/20221211/v0.2/QEMU/  
- 软件源：默认  
- CPU核数：8  
- 内存大小：8G  
- qemu启动参数：  
    ```shell
    qemu-system-riscv64 \
    -nographic -machine virt  \
    -smp 8 -m 8G \
    -audiodev pa,id=snd0 \
    -kernel fw_payload_oe_qemuvirt.elf \
    -bios none \
    -drive file=mugen_ready.qcow2,format=qcow2,id=hd0 \
    -object rng-random,filename=/dev/urandom,id=rng0 \
    -device virtio-rng-device,rng=rng0 \
    -device virtio-blk-device,drive=hd0 \
    -device virtio-net-device,netdev=usernet \
    -netdev user,id=usernet,hostfwd=tcp::"ssh_port"-:22 \
    -device qemu-xhci -usb -device usb-kbd -device usb-tablet -device usb-audio,audiodev=snd0 \
    -append 'root=/dev/vda1 rw console=ttyS0 swiotlb=1 loglevel=3 systemd.default_timeout_start_sec=600 selinux=0 highres=off mem=8192M earlycon' 
    ```
- 附加硬盘qemu参数：
    ```shell
    -drive file=disk"self.id-i".qcow2,format=qcow2,id=hd"i" -device virtio-blk-pci,drive=hd"i"
    ```
    self.id：测试时为对应虚拟机的id  
    i：测试时为某一虚拟机的硬盘序号  
- mugen_ready.qcow2处理  
    mugen_ready.qcow2由原始镜像openEuler-22.03-V2-base-qemu-testing.qcow2安装git和mugen依赖而来  
## 测试结果说明  
### 测试结果文件结构  
- [logs文件夹](https://gitee.com/yunxiangluo/openeuler-riscv-2203-v2-test/tree/master/Auto_Testing/1211-22.03testing/logs)：所有测试用例的日志文件  
- [logs_failed文件夹](https://gitee.com/yunxiangluo/openeuler-riscv-2203-v2-test/tree/master/Auto_Testing/1211-22.03testing/logs_failed)：所有未通过测试用例的日志文件  
- [result.csv](https://gitee.com/yunxiangluo/openeuler-riscv-2203-v2-test/blob/master/Auto_Testing/1211-22.03testing/result.csv):测试结果的详细数据统计  
- [failureCause.csv](https://gitee.com/yunxiangluo/openeuler-riscv-2203-v2-test/blob/master/Auto_Testing/1211-22.03testing/failureCause.csv)：测试未通过原因的初步分析和归类  
## 测试结果  
- 相对此前的oE自动化测试，本次测试扩展了测试范围，测试了范围内测试套中所有测试用例（不包括描述文件中指定需要多机/网卡资源的用例），导致未通过用例比例比此前几次测试大。  