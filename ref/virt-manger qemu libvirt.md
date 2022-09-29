---
date created: 2022-04-08 10:21
---

[Virt-Manager](https://virt-manager.org/) 是提供虚拟机管理服务的 libvirt 库的图形用户前端。 Virt-manager 界面使用户无需通过终端即可轻松创建、删除和操作虚拟机。

Virt-manager 主要支持 KVM，但它可以与 Xen 和 LXC 等其他虚拟机管理程序一起使用。

> **KVM** ， [基于内核的虚拟机](https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine "wikipedia:基于内核的虚拟机") ，是一个 [管理程序](https://en.wikipedia.org/wiki/hypervisor "维基百科：管理程序") 内置在 Linux 内核 它在目的上类似于 [Xen](https://wiki.archlinux.org/title/Xen "辛") ，但运行起来要简单得多。 与使用仿真的原生 [QEMU](https://wiki.archlinux.org/title/QEMU "QEMU") ，KVM 是 QEMU 的一种特殊操作模式，它使用 CPU 扩展 ( [HVM](https://en.wikipedia.org/wiki/Hardware-assisted_virtualization "维基百科：硬件辅助虚拟化") ) 通过内核模块进行虚拟化。
>
> 使用 KVM，可以运行多个运行未经修改的 GNU/Linux、Windows 或任何其他操作系统的虚拟机。 （有关详细信息，请参阅 [访客支持状态](https://www.linux-kvm.org/page/Guest_Support_Status) 。）每个虚拟机都有私有虚拟化硬件：网卡、磁盘、显卡等。

> ## 一般 KVM 信息
>
> ### KVM 和 Xen 有什么区别？
>
> Xen 是一个外部管理程序； 它承担对机器的控制并在客人之间分配资源。 另一方面，KVM 是 Linux 的一部分，使用常规的 Linux 调度程序和内存管理。 这意味着 KVM 更小且更易于使用； 它也更具特色； 例如，KVM 可以将客户机交换到磁盘以释放 RAM。
>
> KVM 仅在支持 x86 hvm（vt/svm 指令集）的处理器上运行，而 Xen 还允许使用称为准虚拟化的技术在非 hvm x86 处理器上运行修改后的操作系统。 KVM 不支持 CPU 的半虚拟化，但可能支持设备驱动程序的半虚拟化以提高 I/O 性能。
>
> ### KVM和VMware有什么区别？
>
> VMware 是专有产品。 KVM 是在 GPL 下发布的自由软件。
>
> ### KVM 和 QEMU 有什么区别？
>
> QEMU 使用仿真； KVM 使用处理器扩展 (HVM) 进行虚拟化。[[virt-manger qemu libvirt#^9ac3bb)
> “QEMU 是一个通用的开源机器模拟器和虚拟器”。
> 当用作机器模拟器时，QEMU 可以在另一台机器（例如您的 x86 PC）上运行为一台机器（例如 ARM 板）制作的操作系统和程序。 通过使用动态翻译，它实现了非常好的性能。
> QEMU 可以使用 [Xen](https://wiki.archlinux.org/title/Xen "辛") 或 [KVM](https://wiki.archlinux.org/title/KVM "虚拟机") 来使用 CPU 扩展 ( [HVM](https://en.wikipedia.org/wiki/Hardware-assisted_virtualization "维基百科：硬件辅助虚拟化") ) 进行虚拟化。 当用作虚拟器时，QEMU 通过直接在主机 CPU 上执行来宾代码来实现接近原生的性能。

^d90d82


## KVM是什么意思？

基于内核的虚拟机 Kernel-based Virtual Machine（KVM）是一种内建于 Linux® 中的开源[虚拟化](https://www.redhat.com/zh/topics/virtualization/what-is-virtualization)技术。具体而言，KVM 可帮助您将 Linux 转变为[虚拟机监控程序](https://zh.wikipedia.org/wiki/Hypervisor)，使主机计算机能够运行多个隔离的虚拟环境，即虚拟客户机或虚拟机（VM）。

KVM 是 Linux 的一部分。Linux 2.6.20 或更新版本包括 KVM。KVM 于 2006 年首次公布，并在一年后合并到主流 Linux 内核版本中。由于 KVM 属于现有的 Linux 代码，因此它能立即享受每一项新的 Linux 功能、修复和发展，无需进行额外工程。

## KVM是如何运行的？

KVM 将 Linux 转变为 1 类（裸机恢复）虚拟机监控程序。**所有虚拟机监控程序都需要一些操作系统层面的组件才能运行虚拟机，如内存管理器、进程调度程序、输入/输出（I/O）堆栈、设备驱动程序、安全管理器以及网络堆栈等。由于 KVM 是 Linux 内核的一部分，因此所有这些组件它都有。每个虚拟机都像普通的 Linux 进程一样实施，由标准的 Linux 调度程序进行调度，并且使用专门的虚拟硬件，如网卡、图形适配器、CPU、内存和磁盘等。** ^9ac3bb

## 安装

[安装](https://wiki.archlinux.org/title/Install "安装") [virt-manager](https://archlinux.org/packages/?name=virt-manager) [qemu](https://archlinux.org/packages/?name=qemu) [libvirt](https://archlinux.org/packages/?name=libvirt) [edk2-ovmf](https://archlinux.org/packages/?name=edk2-ovmf) [dnsmasq](https://archlinux.org/packages/?name=dnsmasq) [iptables-](https://archlinux.org/packages/?name=iptables-nft) 。

[启用/](https://wiki.archlinux.org/title/Enable/start "启用/启动") 启动 `libvirtd.service`.

您可以检查 [设备状态](https://wiki.archlinux.org/title/Unit_status "单位状态") 以确保服务正在运行。

## 配置

To use as a normal user without [root](https://wiki.archlinux.org/title/Root "Root") we need to configure KVM, this will also enable the libvirt networking components.
为了可以在没有 `root` 权限的情况下以普通用户使用, 我们需要配置 `KVM`. 这也将启用 `libvirt` 网络组件。
将 UNIX 域套接字所有权设置为 libvirt，并将 UNIX 套接字权限设置为读写。
取消下列注释

```edit
/etc/libvirt/libvirtd.conf
---
...
 unix_sock_group = 'libvirt'
 ...
 unix_sock_rw_perms = '0770'
 ...
```

将您的用户添加到 libvirt [用户组](https://wiki.archlinux.org/title/User_group "用户组") 。

```shell
sudo usermod -a -G libvirt $USER
groups $USER # for checking
```

将您的用户添加到 `/etc/libvirt/qemu.conf`. 否则，QEMU 在尝试访问本地驱动器时会给出权限被拒绝错误。

搜索 `user == "root"`或者 `group = "root"`, 取消注释两个条目并更改 `root`到您的用户名或 ID。 编辑后，它应该如下所示。

```
/etc/libvirt/qemu.conf

# Some examples of valid values are:
#
#       user = "qemu"   # A user named "qemu"
#       user = "+0"     # Super user (uid=0)
#       user = "100"    # A user named "100" or a user with uid=100
#
user = _username_

# The group for QEMU processes run by the system instance. It can be
# specified in a similar way to user.
group = _username_
```

[Restart](https://wiki.archlinux.org/title/Restart "Restart") `libvirtd.service`.

# Run `virt-manager

![](./attachments/Pasted%20image%2020220407140135.png)
右键 `QEMU/KVM` 选择 `NEW` 或者 左上角 加号➕

![](../attachments/Pasted%20image%2020220407225332.png)
![](../attachments/Pasted%20image%2020220407225341.png)
`browse`
![](../attachments/Pasted%20image%2020220407225411.png)
`Browse Local`
![](../attachments/Pasted%20image%2020220407225440.png)
![](../attachments/Pasted%20image%2020220407225449.png)
![](../attachments/Pasted%20image%2020220407225459.png)
![](../attachments/Pasted%20image%2020220407225523.png)
![](../attachments/Pasted%20image%2020220407225531.png)
