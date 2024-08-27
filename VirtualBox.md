# VirtualBox

## Increase size of virtual drive
In general two steps are taken:
1. change size of the vdi file - as if you were going to exchange the HD of the pc...
[This](https://dev.to/ech0server/how-to-resize-a-virtualbox-linux-vdi-disk-under-windows-host-2d1p) is a very comprehensive guide.
2. partition the added space

### First step - examples
* host: Windows 7 Pro; VirtualBox: 5.1.2.

  `H:\>"c:\Program Files\Oracle\VirtualBox\VBoxManage.exe" modifyhd "u:\ALESSIO\VirtualMachines\ubuntu_test\ubuntu_test.vdi" --resize 200000`

  running process:

  `0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%`

### Second step - examples
* guest: Ubuntu 16.04
  This operation is done with `gparted`, a utility for managing HD partitions available in Linux. In order to operate on the HD without issues, it is necessary to access the machine via the ISO CD.
  1. insert the ISO CD of Ubuntu 16.04. When asked: `Try Ubuntu`
  1. you may need to delete the swap partition (from [askubuntu](https://askubuntu.com/questions/349987/do-i-have-to-move-swap-partition-to-the-right-side), credits Sadi):
      * Select the partition, right-click `Swapoff` (to unmount the swap partition so that you can perform operations on it);
      * Delete Swap partition, which will create a larger unallocated space at the end of the partition you want to expand;
      * Create one or more partitions as you need and then re-create the Swap partition at the end.

## Rebuild the guest addition ISO from repo
It may happen that there is the need to re-build the guest addition ISO, e.g. because:
* shared folders are empty;

In a LINUX (Ubuntu) guest OS, you can do this via terminal line (see [stackexchange](https://unix.stackexchange.com/questions/570240/virtualbox-guest-additions-error-kernel-configuration-is-invalid)):
1. Run `sudo apt install virtualbox-guest-additions-iso` to get the latest repositories;
1. The guest iso will be found in `/usr/share/virtualbox/VBoxGuestAdditions.iso`;
1. Create a mount point and mount iso: `sudo mkdir -p /mnt/cdrom && sudo mount /usr/share/virtualbox/VBoxGuestAdditions.iso /mnt/cdrom`;
1. Navigate to iso and install: `cd /mnt/cdrom && sudo sh ./VBoxLinuxAdditions.run --nox11`.

## Change path/name of shared folders on guest OS
The path and suffixes of shared folders in the guest OS can be controlled in the host OS directly by VirtualBox.
Please open a terminal and type (please note the use of the full path to `VBoxManage` and the use of the double-quotes character):
```
"C:\Program Files\Oracle\VirtualBox\VBoxManage" guestproperty set [VM Name] /VirtualBox/GuestAdd/SharedFolders/MountPrefix /
"C:\Program Files\Oracle\VirtualBox\VBoxManage" guestproperty set [VM Name] /VirtualBox/GuestAdd/SharedFolders/MountDIR /home/user
```

## References
* [askubuntu](https://askubuntu.com/questions/1039465/virtualbox-storage-mount-directory-prefix-verr-permission-denied);
* [VBox Manual: guest properties](https://docs.oracle.com/en/virtualization/virtualbox/6.0/user/vboxmanage-guestproperty.html);
* [VBox Manual: manually add/remove shared folders](https://docs.oracle.com/en/virtualization/virtualbox/6.0/user/vboxmanage-sharedfolder.html);
* [VBox Manual: generalities about shared folders](https://docs.oracle.com/en/virtualization/virtualbox/6.0/user/sharedfolders.html);
