# Notes about environment in VMs
This file summarises some infos concerning our VM Linux machines.

## Ubuntu 22.04 LTS on Win machine WS0040
Useful paths
| *VM Path* | *Description* | 
| --- | --- |
| `/home/<username>` | home folder of each user. Desktop is found at `/home/<username>/Desktop` |
| `/mnt/DATA/<username>` | parent folder for storing data (e.g. from simulation) of each user. |
| `/mnt/hgfs/PCNAO` | mount path of shared disk `P:`. Read only! |
| `/mnt/hgfs/TCNAO` | mount path of shared disk `T:`. Read only! |
| `/mnt/hgfs/Area_Ricerca` | mount path of shared folder `S:\Area Ricerca`. |
| `/mnt/hgfs/VBSHARE` | mount path of shared folder `D:\VMs\VBSHARE`. |

Useful exes:
| *Path* | *Description* | 
| --- | --- |
| `/mnt/hgfs/TCNAO/MADX/5.07.00/madx-linux64.gnu` | MADX ver 5.07.00 |

# Some useful commands
* add new group `$ sudo addgroup <myGroupName>`  (from [link](https://subscription.packtpub.com/book/networking-&-servers/9781785883064/1/ch01lvl1sec12/creating-a-group));
* add existing user to existing group: `$ sudo usermod -aG <myGroupName> <myUserName>` (from [link](https://www.howtogeek.com/50787/add-a-user-to-a-group-or-second-group-on-linux/));
