---
layout: post
title: "Why the need for the VMware Tools"
excerpt: "Trying to give a little reasoning behind every virtual infrastructure administrators request."
tags: [vmware,vcenter,vmware tools,drivers]
comments: true
image:
  feature: vSphere6.0.jpg

---

More frequently than many of us would ever imagine, we see VMs at enterprise levels that don't have the VMware Tools installed in their VMs. More often this is found in Linux virtual machines, but it happens on all types of VMs no matter what.
I keep getting asked, "Why is it so important to have the VMware tools installed?" or "What does having them install really benefit me?"

I get it, you don't want to just install some crap because some bearded man told you to. But seriously, there are plenty of benefits for such a trivial install.

Directly from the [source](https://pubs.vmware.com/vsphere-60/topic/com.vmware.ICbase/PDF/vsphere-esxi-vcenter-server-601-virtual-machine-admin-guide.pdf), here are some of the benefits.

> * Significantly faster graphics performance and Windows Aero on operating systems that support Aero
* The Unity feature, which enables an application in a virtual machine to appear on the host desktop like any other application window
* Shared folders between host and guest file systems
* Copying and pasting text, graphics, and files between the virtual machine and the host or client desktop
* Improved mouse performance
* Synchronization of the clock in the virtual machine with the clock on the host or client desktop
* Scripting that helps automate guest operating system operations
* Runs pre-freeze and post-thaw quiescing scripts
* Enables capturing quiesced snapshots of guest operating systems
* Periodically collects network, disk, and memory usage information from the guest operating system and sends it to ESXi hosts.
* Sends a heartbeat to each virtual machine every second and collects guest heartbeat information from guest operating systems. VMware HA uses the heartbeat information to determine virtual machine availability.
* Transports the OVF environment to guest operating systems using the guest OS environment variable *guestinfo.ovfEnv* that contains the XML document.
>
Although the guest operating system can run without VMware Tools, many VMware features are not available until you install VMware Tools. For example, if you do not have VMware Tools installed in your virtual machine, you cannot get heartbeat information from guest operating systems or cannot use the shutdown or restart options from the toolbar. You can only use the power options and you have to shut down your guest operating systems from each virtual machine console. You cannot use VMware Tools for connecting and disconnecting virtual devices, and shrinking virtual disks.

## VMware Tools Service

>
The VMware Tools service starts when the guest operating system starts. The service passes information between host and guest operating systems.
This program, which runs in the background, is called vmtoolsd.exe in Windows guest operating systems, vmware-tools-daemon in Mac OS X guest operating systems, and vmtoolsd in Linux, FreeBSD, and Solaris guest operating systems. The VMware Tools service performs the following tasks:
* Passes messages from the host to the guest operating system.
* Provides support for customization of guest operating systems as a part of the vCenter Server and other VMware products.
* Provides support for guest operating system-bound calls created with the VMware VIX API, except in Mac OS X guest operating systems.
* Runs scripts that help automate guest operating system operations. The scripts run when the power state of the virtual machine changes.
* Synchronizes the time in the guest operating system with the time on the host.
* In Windows guest operating systems, allows the pointer to move freely between the guest and the vSphere Web Client.
On Linux guest operating systems that run Xorg 1.8 and later, this functionality is available as a
standard feature.
* In Windows and Mac OS X guest operating systems, fits the screen display resolution of the guest to the screen resolution of the vSphere Web Client, if running in full screen mode. If running in windowed mode, fits the screen resolution of the guest to the size of the window on the client or host.
* In Windows and Linux guest operating systems, helps create the quiesced snapshots used by certain backup applications.
* In Windows, Linux, Solaris, and FreeBSD guest operating systems, runs custom power-on script in the virtual machine when you shut down or restart the guest operating system.
* Is one of the processes that sends a heartbeat to the VMware product to indicate that the guest operating system is running. When the virtual machine runs under ESXi or vCenter Server, a gauge for this heartbeat appears in the management interface.
* Provides support for guest operating on Windows and Linux created using the VMware VIX API, except in Mac OS X guest operating systems. For information VIX API, see the vSphere API Reference documentation.

>
## VMware Tools Device Drivers

> Device drivers optimize mouse operations and improve sound, graphics, and networking performance. If you do a custom VMware Tools installation or reinstallation, you can choose which drivers to install.

>Which drivers are installed when you install VMware Tools also depends on the guest operating system and the VMware product. For detailed information about the features or functionality that these drivers enable, including configuration requirements, best practices, and performance, see the documentation for your VMware product. The following device drivers can be included with VMware Tools.
>
|:--------|:-------:|
| SVGA driver | This virtual driver enables 32-bit displays, high display resolution, and significantly faster graphics performance. When you install VMware Tools, a virtual SVGA driver replaces the default VGA driver, which allows for only 640 X 480 resolution and 16-color graphics. On Windows guest operating systems whose operating system is Windows Vista or later, the VMware SVGA 3D (Microsoft - WDDM) driver is installed. This driver provides the same base functionality as the SVGA driver, and it adds Windows Aero support.|
| SCSI driver | A VMware Paravirtual SCSI driver is included for use with paravirtual SCSI devices. Drivers for other storage adapters are either bundled with the operating system, or they are available from third-party vendors. For example, Windows Server 2008 defaults to LSI Logic SAS, which provides the best performance for that operating system. In this case, the LSI Logic SAS driver provided by the operating system is used. |
| Paravirtual SCSI driver | This driver for VMware Paravirtual SCSI adapters enhances the performance of some virtualized applications |
| VMXNet NIC drivers | The vmxnet and vmxnet3 networking drivers improve network performance. Which driver is used depends on how you configure device settings for the virtual machine. Search the VMware Knowledge Base for information on which guest operating systems support these drivers. When you install VMware Tools, a VMXNet NIC driver replaces the default vlance driver. |
| Mouse driver | The virtual mouse driver improves mouse performance. This driver is required if you use some third-party tools such as Microsoft Terminal Services. |
| Audio driver | This sound driver is required for all 64-bit Windows guest operating systems and 32-bit Windows Server 2003, Windows Server 2008, and Windows Vista guest operating systems. |
| Guest Introspection drivers | The two Guest Introspection drivers are the NSX File Introspection driver and the Network Introspection driver. The NSX File Introspection driver uses the hypervisor to perform antivirus scans without a bulky agent. This strategy avoids resource bottlenecks and optimizes memory use. The NSX Network Introspection driver supports NSX for vSphere Activity Monitoring. You can install the two drivers separately. When you install VMware Tools, by default, the Guest Introspection drivers are not installed. |
| Memory control driver | This driver is required for memory ballooning and is recommended if you use VMware vSphere. Excluding this driver hinders the memory management capabilities of the virtual machine in a vSphere deployment |
| Modules and drivers that support making automatic backups of virtual machines | If the guest operating system is Windows Vista, Windows Server 2003, or other newer Windows operating systems, a Volume Shadow Copy Services (VSS) module is installed. For other, older Windows operating systems, the Filesystem Sync driver is installed. These modules allow external third-party backup software that is integrated with vSphere to create application consistent snapshots. During the snapshotting process, certain processes are paused and virtual machine disks are quiesced. |
| VMCI and VMCI Sockets drivers | The Virtual Machine Communication Interface driver allows fast and efficient communication between virtual machines and the hosts they run on. Developers can write client-server applications to the VMCI Sock (vsock) interface to make use of the VMCI virtual device. |
| VMware drivers for Linux | The drivers for Linux are automatically installed during your operating system installation, eliminating the need to separately install drivers after OS installation. VMware actively maintains the source code for VMware paravirtual drivers and kernel modules, and any Linux distributions creating new OS releases will automatically include the latest VMware drivers. VMware does not recommend deleting or replacing existing inbox drivers for Linux that are distributed by your OS vendors. Deleting or replacing these drivers could cause conflict with future updates to the drivers. Contact your OS vendor or OS community for availability of specific updates to drivers. See http://kb.vmware.com/kb/2073804 for information about availability, maintenance, and support policy for inbox drivers for Linux. |


So, install the damn tools. It'll help you out at least one time.
