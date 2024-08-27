# Notes about environment in VMs
This file summarises some infos concerning our VM Linux machines.

## Ubuntu 22.04 LTS on Win machine WS0040
**!! THIS MACHINE IS NO LONGER AVAILABLE !!**

The material presented here is anyway left for reference.

### Useful paths
| *VM Path* | *Description* | 
| --- | --- |
| `/home/<username>` | home folder of each user. Desktop is found at `/home/<username>/Desktop` |
| `/mnt/DATA/<username>` | parent folder for storing data (e.g. from simulation) of each user. |
| `/mnt/hgfs/PCNAO` | mount path of shared disk `P:`. Read only! (not available as Win user Inventor) |
| `/mnt/hgfs/TCNAO` | mount path of shared disk `T:`. Read only! |
| `/mnt/hgfs/Area_Ricerca` | mount path of shared folder `S:\Area Ricerca`. (not available as Win user Inventor) |
| `/mnt/hgfs/VBSHARE` | mount path of shared folder `D:\VMs\VBSHARE`. |

### Useful exes
| *Path* | *Description* | 
| --- | --- |
| `/mnt/hgfs/TCNAO/ARicerca/MADX/5.07.00/madx-linux64-gnu` | MADX ver 5.07.00 |
| `/usr/local/FLUKA/INFN/2021.2.8` | INFN Fluka 2021.2.8 |

### Groups
| *group name* | *Description* |
| --- | --- |
| `fluka` | people able to run FLUKA on the VM |
| `rwdata` | people able to read and write on the DATA path |

### Adding a new user
* add them to the necessary groups;
* create a dedicated folder in `DATA`, e.g.: `drwxrwxr-x 2 amereghe amereghe  4096 gen 20 15:20 amereghe/`

### Environment variables
```
# .bashrc
# terminal line behavior:
# - do not escape $ when tabbing:
shopt -s direxpand
# use local numeric interpretation as default C
export LC_NUMERIC=C
# env vars for FLUKA
export FLUPRO=/usr/local/FLUKA/INFN/2021.2.9
export FLUKA=${FLUPRO}
export FLUFOR=gfortran
# some useful paths
export PCNAO=/mnt/hgfs/PCNAO
export TCNAO=/mnt/hgfs/TCNAO
export AREA_RICERCA=/mnt/hgfs/Area_Ricerca
export VBSHARE=/mnt/hgfs/VBSHARE
export DATA=/mnt/DATA/$USER
# expand PATH beyond defaults
export PATH=${PATH}:${TCNAO}/ARicerca/MADX/5.06.01:${FLUKA}
```

### File System Table
```
# Use shared folders between VMWare guest and host
.host:/         /mnt/hgfs    fuse.vmhgfs-fuse    defaults,allow_other     0    0
# permanently mount DATA readable and writeable by every user
/dev/sda4	/mnt/DATA	ext4	defaults	0	0
```

## Ubuntu 22.04 LTS on Win machine WS0024
**!! THIS MACHINE IS NO LONGER AVAILABLE !!**

The material presented here is anyway left for reference.

### Useful paths
| *VM Path* | *Description* | 
| --- | --- |
| `/home/<username>` | home folder of each user. Desktop is found at `/home/<username>/Desktop` |
| `/mnt/DATA/<username>` | parent folder for storing data (e.g. from simulation) of each user. |
| `/mnt/hgfs/PCNAO` | mount path of shared disk `P:`. Read only! |
| `/mnt/hgfs/TCNAO` | mount path of shared disk `T:`. Read only! |
| `/mnt/hgfs/Area_Ricerca` | mount path of shared folder `S:\Area Ricerca`. |
| `/mnt/hgfs/ScambioClinicaTecnica` | mount path of shared folder `S:\ScambioClinicaTecnica`. |
| `/mnt/hgfs/VBSHARE` | mount path of shared folder `U:\VMs\VBSHARE`. |

### Useful exes
| *Path* | *Description* | 
| --- | --- |
| `/mnt/hgfs/TCNAO/ARicerca/MADX/5.07.00/madx-linux64-gnu` | MADX ver 5.07.00 |
| `/usr/local/FLUKA/INFN/2021.2.9` | INFN Fluka 2021.2.9 |

### Groups
| *group name* | *Description* |
| --- | --- |
| `fluka` | people able to run FLUKA on the VM |
| `rwdata` | people able to read and write on the DATA path |

### Adding a new user
* add them to the necessary groups;
* create a dedicated folder in `DATA`, e.g.: `drwxrwxr-x 2 amereghe amereghe  4096 gen 20 15:20 amereghe/`

### Environment variables
```
# .bashrc
# terminal line behavior:
# - do not escape $ when tabbing:
shopt -s direxpand
# use local numeric interpretation as default C
export LC_NUMERIC=C
# env vars for FLUKA
export FLUPRO=/usr/local/FLUKA/INFN/2021.2.9
export FLUKA=${FLUPRO}
export FLUFOR=gfortran
# some useful paths
export PCNAO=/mnt/hgfs/PCNAO
export TCNAO=/mnt/hgfs/TCNAO
export AREA_RICERCA=/mnt/hgfs/Area_Ricerca
export ScambioClinicaTecnica=/mnt/hgfs/ScambioClinicaTecnica
export VBSHARE=/mnt/hgfs/VBSHARE
export DATA=/mnt/DATA/$USER
# expand PATH beyond defaults
export PATH=${PATH}:${TCNAO}/ARicerca/MADX/5.06.01:${FLUKA}
```

### File System Table
```
# Use shared folders between VMWare guest and host
.host:/         /mnt/hgfs    fuse.vmhgfs-fuse    defaults,allow_other     0    0
# permanently mount DATA readable and writeable by every user
/dev/sda4	/mnt/DATA	ext4	defaults	0	0
```
