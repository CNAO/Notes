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
