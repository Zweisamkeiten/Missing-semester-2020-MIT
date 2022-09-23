---
date created: 2022-04-08 10:42
---

Libvirt 是一组软件，提供了一种方便的方式来管理虚拟机和其他虚拟化功能，例如存储和网络接口管理。 这些软件包括一个长期稳定的 C API、一个守护进程 (libvirtd) 和一个命令行实用程序 (virsh)。 libvirt 的主要目标是提供单一方式来管理多个不同的虚拟化提供程序/管理程序，例如 [KVM/QEMU](https://wiki.archlinux.org/title/QEMU "QEMU") 、 [Xen](https://wiki.archlinux.org/title/Xen "辛") 、 [LXC](https://wiki.archlinux.org/title/LXC "LXC") 、 [OpenVZ](https://openvz.org) 或 [VirtualBox](https://wiki.archlinux.org/title/VirtualBox "虚拟盒子") [管理程序](https://wiki.archlinux.org/title/Category:Hypervisors "类别：管理程序") （ [等等](https://libvirt.org/drivers.html) ）。 ^6cdbc5

libvirt 的一些主要功能包括：

- **虚拟机管理** ：启动、停止、暂停、保存、恢复和迁移等各种域生命周期操作。 许多设备类型的热插拔操作，包括磁盘和网络接口、内存和 CPU。
- **远程机器支持** ：所有 libvirt 功能都可以在任何运行 libvirt 守护进程的机器上访问，包括远程机器。 远程连接支持多种网络传输，最简单的是 SSH，不需要额外的显式配置。
- **存储管理** ：任何运行 libvirt 守护进程的主机都可用于管理各种类型的存储：创建各种格式的文件映像（qcow2、vmdk、raw，...），挂载 NFS 共享，枚举现有的 LVM 卷组，创建新的 LVM卷组和逻辑卷、分区原始磁盘设备、装载 iSCSI 共享等等。
- **网络接口管理** ：任何运行 libvirt 守护进程的主机都可以用来管理物理和逻辑网络接口。 枚举现有接口，以及配置（和创建）接口、网桥、VLAN 和绑定设备。
- **虚拟 NAT 和基于路由的网络** ：任何运行 libvirt 守护进程的主机都可以管理和创建虚拟网络。 Libvirt 虚拟网络使用防火墙规则充当路由器，为虚拟机提供对主机网络的透明访问。
