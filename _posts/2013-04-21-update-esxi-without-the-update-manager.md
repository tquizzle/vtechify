---
layout: post
title: "Update ESXi without the Update Manager"
excerpt: "No vCenter with Update Manager? No Problem."
tags: [ESXi, Host, Patch, Upgrade, VIB, VUM]
comments: true
image:
  feature: vSphere6.0.jpg
---

![vSphere 5][1]
{: .image-pull-right}

I’ve needed to do this quite a few times. Especially in my home lab and with a couple of clients whom only have a single ESXi server and no vCenter server.

I felt like I should jot it down and use that as a reference later. What is outlined below is the simplest way that I have found to upload and install patches (VMware now calls them VIBs) to an ESXi host.

### Get Started

* Download patches necessary from the [VMware Patch Portal](http://www.vmware.com/patchmgr/findPatch.portal) for your version of ESXi
* Enable SSH for your ESXi Host
* Put host into Maintenance Mode
* Transfer the file(s) over to a Mounted datastore. I used [SCP](http://winscp.net/eng/download.php)
* Once you've uploaded the file(s) this is now considered your Local Depot Repository

### Patch

So, the files have now been transferred over to a mounted datastore now so its time to begin the upload and patch.

You can do this many ways, either using PowerCLI, Remote CLI through the VMA, SSH into the host itself or directly on the console. I’ll be using SSH in my example.

{% highlight bash %}
esxcli software vib install -d /vmfs/volumes/[DATASTORE]/[PATCH_FILE].zip
{% endhighlight %}

Once the patches are installed you’ll see something like this:

{% highlight bash %}
Installation Result
Message: The update completed successfully, but the system needs to be rebooted for the changes to be effective.
Reboot Required: true
VIBs Installed: VMware_bootbank_esx-base_5.0.0-0.4.504890
VIBs Removed: VMware_bootbank_esx-base_5.0.0-0.3.474610
VIBs Skipped: VMware_bootbank_ata-pata-amd_0.3.10-3vmw.500.0.0.469512, VMware_bootbank_ata-pata-atiixp_0.4.6-3vmw.500.0.0.469512, VMware_bootbank_ata-pata-cmd64x_0.2.5-3vmw.500.0.0.469512, VMware_bootbank_ata-pata-hpt3x2n_0.3.4-3vmw.500.0.0.469512, VMware_bootbank_ata-pata-pdc2027x_1.0-3vmw.500.0.0.469512, VMware_bootbank_ata-pata-serverworks_0.4.3-3vmw.500.0.0.469512, VMware_bootbank_ata-pata-sil680_0.4.8-3vmw.500.0.0.469512, VMware_bootbank_ata-pata-via_0.3.3-2vmw.500.0.0.469512, VMware_bootbank_block-cciss_3.6.14-10vmw.500.0.0.469512, VMware_bootbank_ehci-ehci-hcd_1.0-3vmw.500.0.0.469512, VMware_bootbank_esx-tboot_5.0.0-0.0.469512, VMware_bootbank_ima-qla4xxx_2.01.07-1vmw.500.0.0.469512, VMware_bootbank_ipmi-ipmi-devintf_39.1-4vmw.500.0.0.469512, VMware_bootbank_ipmi-ipmi-msghandler_39.1-4vmw.500.0.0.469512, VMware_bootbank_ipmi-ipmi-si-drv_39.1-4vmw.500.0.0.469512, VMware_bootbank_misc-cnic-register_1.1-1vmw.500.0.0.469512, VMware_bootbank_misc-drivers_5.0.0-0.0.469512, VMware_bootbank_net-be2net_4.0.88.0-1vmw.500.0.0.469512, VMware_bootbank_net-bnx2_2.0.15g.v50.11-5vmw.500.0.0.469512, VMware_bootbank_net-bnx2x_1.61.15.v50.1-1vmw.500.0.0.469512, VMware_bootbank_net-cnic_1.10.2j.v50.7-2vmw.500.0.0.469512, VMware_bootbank_net-e1000_8.0.3.1-2vmw.500.0.0.469512, VMware_bootbank_net-e1000e_1.1.2-3vmw.500.0.0.469512, VMware_bootbank_net-enic_1.4.2.15a-1vmw.500.0.0.469512, VMware_bootbank_net-forcedeth_0.61-2vmw.500.0.0.469512, VMware_bootbank_net-igb_2.1.11.1-3vmw.500.0.0.469512, VMware_bootbank_net-ixgbe_2.0.84.8.2-10vmw.500.0.0.469512, VMware_bootbank_net-nx-nic_4.0.557-3vmw.500.0.0.469512, VMware_bootbank_net-r8168_8.013.00-3vmw.500.0.0.469512, VMware_bootbank_net-r8169_6.011.00-2vmw.500.0.0.469512, VMware_bootbank_net-s2io_2.1.4.13427-3vmw.500.0.0.469512, VMware_bootbank_net-sky2_1.20-2vmw.500.0.0.469512, VMware_bootbank_net-tg3_3.110h.v50.4-4vmw.500.0.0.469512, VMware_bootbank_ohci-usb-ohci_1.0-3vmw.500.0.0.469512, VMware_bootbank_sata-ahci_3.0-6vmw.500.0.0.469512, VMware_bootbank_sata-ata-piix_2.12-4vmw.500.0.0.469512, VMware_bootbank_sata-sata-nv_3.5-3vmw.500.0.0.469512, VMware_bootbank_sata-sata-promise_2.12-3vmw.500.0.0.469512, VMware_bootbank_sata-sata-sil_2.3-3vmw.500.0.0.469512, VMware_bootbank_sata-sata-svw_2.3-3vmw.500.0.0.469512, VMware_bootbank_scsi-aacraid_1.1.5.1-9vmw.500.0.0.469512, VMware_bootbank_scsi-adp94xx_1.0.8.12-6vmw.500.0.0.469512, VMware_bootbank_scsi-aic79xx_3.1-5vmw.500.0.0.469512, VMware_bootbank_scsi-bnx2i_1.9.1d.v50.1-3vmw.500.0.0.469512, VMware_bootbank_scsi-fnic_1.5.0.3-1vmw.500.0.0.469512, VMware_bootbank_scsi-hpsa_5.0.0-17vmw.500.0.0.469512, VMware_bootbank_scsi-ips_7.12.05-4vmw.500.0.0.469512, VMware_bootbank_scsi-lpfc820_8.2.2.1-18vmw.500.0.0.469512, VMware_bootbank_scsi-megaraid-mbox_2.20.5.1-6vmw.500.0.0.469512, VMware_bootbank_scsi-megaraid-sas_4.32-1vmw.500.0.0.469512, VMware_bootbank_scsi-megaraid2_2.00.4-9vmw.500.0.0.469512, VMware_bootbank_scsi-mpt2sas_06.00.00.00-5vmw.500.0.0.469512, VMware_bootbank_scsi-mptsas_4.23.01.00-5vmw.500.0.0.469512, VMware_bootbank_scsi-mptspi_4.23.01.00-5vmw.500.0.0.469512, VMware_bootbank_scsi-qla2xxx_901.k1.1-14vmw.500.0.0.469512, VMware_bootbank_scsi-qla4xxx_5.01.03.2-3vmw.500.0.0.469512, VMware_bootbank_uhci-usb-uhci_1.0-3vmw.500.0.0.469512, VMware_locker_tools-light_5.0.0-0.3.474610
{% endhighlight %}

Now, reboot your host and you should notice that the system was patched.

### Multiple Patch Info

If you need to update multiple patches at the same time, you may do so but only in succession starting with the oldest first.

On a recent install I found that I needed to install 3 patches.

* ESXi510-201210001.zip
* ESXi510-201212001.zip
* ESXi510-201303001.zip

That’s the order I patched them in and then rebooted a single time and now my host at my lab is fully up-to-date.

Thanks to [Chris Colotti’s post](http://www.chriscolotti.us/vmware/vsphere/how-to-patch-vsphere-5-esxi-without-update-manager/) for making perfect sense of all of this.

[1]: http://i2.wp.com/vsphere-land.com/wp-content/uploads/vsphere5-300x160.png