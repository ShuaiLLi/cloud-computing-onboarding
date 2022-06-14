
# 为什么要了解KVM？

在 x86 平台上最热门运用最广泛的虚拟化方案莫过于 KVM（一种 Hypervisor） 了。OpenStack 对 KVM 支持得也最好，因此在学习 OpenStack 之前我们有必要了解KVM。

# KVM简介

基于内核的虚拟机 Kernel-based Virtual Machine（KVM）是一种内建于 Linux 中的开源虚拟化技术。具体而言，KVM 可帮助您将 Linux 转变为虚拟机监控程序，使主机计算机能够运行多个隔离的虚拟环境，即虚拟客户机或虚拟机（VM）。

KVM 是 Linux 的一部分。Linux 2.6.20 或更新版本包括 KVM。KVM 于 2006 年首次公布，并在一年后合并到主流 Linux 内核版本中。由于 KVM 属于现有的 Linux 代码，因此它能立即享受每一项新的 Linux 功能、修复和发展，无需进行额外工程。

# KVM是如何运行的？

KVM 将 Linux 转变为 type-1（裸机虚拟化）虚拟机监控程序。所有虚拟机监控程序都需要一些操作系统层面的组件才能运行虚拟机，如内存管理器、进程调度程序、输入/输出（I/O）堆栈、设备驱动程序、安全管理器以及网络堆栈等。KVM自己有一个内核模块叫 kvm.ko，用于管理虚拟 CPU 和内存，由于 KVM 是 Linux 内核的一部分， 因此其他设备的虚拟化都交给 Linux 内核和Qemu。每个虚拟机都像普通的 Linux 进程一样实施，由标准的 Linux 调度程序进行调度，并且使用专门的虚拟硬件，如网卡、图形适配器、CPU、内存和磁盘等。

说白了，作为一个 Hypervisor，KVM 本身只关注虚拟机调度和内存管理这两个方面。IO 外设的任务交给 Linux 内核和 Qemu。

# libvirt简介

有了KVM之后，我们想要对KVM进行管理就要有相应的管理工具，而 libvirt 就是一套用于管理硬件虚拟化的开源API、守护进程与管理工具。此套组可用于管理KVM、Xen、VMware ESXi、QEMU及其他虚拟化技术。libvirt内置的API广泛用于云解决方案开发中的虚拟机监视器编排层（Orchestration Layer）。

libvirt 包含 3 个组件：后台 daemon 程序 libvirtd（守护进程）、API 库和命令行工具 virsh

- libvirtd是Server进程，负责接收和处理 API 请求

- API 库使得其他人可以开发基于 Libvirt 的高级工具，比如 virt-manager，这是个图形化的 KVM 管理工具

- virsh 是我们经常要用的 KVM 命令行工具

作为 KVM 和 OpenStack 的实施人员，virsh 和 virt-manager 是一定要会用的。
