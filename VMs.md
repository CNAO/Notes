# Notes about environment in VMs
This file summarises some infos concerning our VM Linux machines.

## Ubuntu 22.04 LTS on Win machine WS0040
### Useful paths
| *VM Path* | *Description* | 
| --- | --- |
| `/home/<username>` | home folder of each user. Desktop is found at `/home/<username>/Desktop` |
| `/mnt/DATA/<username>` | parent folder for storing data (e.g. from simulation) of each user. |
| `/mnt/hgfs/PCNAO` | mount path of shared disk `P:`. Read only! |
| `/mnt/hgfs/TCNAO` | mount path of shared disk `T:`. Read only! |
| `/mnt/hgfs/Area_Ricerca` | mount path of shared folder `S:\Area Ricerca`. |
| `/mnt/hgfs/VBSHARE` | mount path of shared folder `D:\VMs\VBSHARE`. |

### Useful exes
| *Path* | *Description* | 
| --- | --- |
| `/mnt/hgfs/TCNAO/MADX/5.07.00/madx-linux64.gnu` | MADX ver 5.07.00 |
| `/usr/local/FLUKA/INFN/2021.2.8` | INFN Fluka 2021.2.8 |

### Groups
| *group name* | *Description* |
| --- | --- |
| `fluka` | people able to run FLUKA on the VM |
| `rwdata` | people able to read and write on the DATA path |

### Environment variables
```
# .bashrc
# env vars for FLUKA
export FLUPRO=/usr/local/FLUKA/INFN/2021.2.8
export FLUKA=/usr/local/FLUKA/INFN/2021.2.8
export FLUFOR=gfortran
```

# Some useful admin commands
* add new group `$ sudo addgroup <myGroupName>`  (from [link](https://subscription.packtpub.com/book/networking-&-servers/9781785883064/1/ch01lvl1sec12/creating-a-group));
* add existing user to existing group: `$ sudo usermod -aG <myGroupName> <myUserName>` (from [link](https://www.howtogeek.com/50787/add-a-user-to-a-group-or-second-group-on-linux/));

# Some useful programs
Nota bene: installation commands are referred to Ubuntu 22.04 LTS
| *name* | *install command* | *comment* |
| --- | --- | --- |
| google chrome | see Notes | web browser |
| emacs | `sudo apt-get install emacs` | text file editor |
| meld | `sudo apt-get install meld` | text file editor - useful for comparing text files |
| git | `sudo apt-get install git` | revision tracking system |
| gparted | `sudo apt-get install gparted` | tool to partition filesystem |
| gcc | `sudo apt-get install gcc` | gnu `C` compiler (includes `libc`) |
| gfortran | `sudo apt-get install gfortran` | gnu `fortran` compiler |
| make | `sudo apt-get install make` | Linux utility to compile exes |

Notes:
* to install google chrome from terminal:
```
cd ~/Downloads
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo chown -Rv _apt:root ./google-chrome-stable_current_amd64.deb
sudo chmod -Rv 700 ./google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
```

# CheatSheet for Installing FLUKA
1. Prepare a `fluka` linux group and add all the concerned users (including `root`): `sudo addgroup fluka; sudo usermod -aG fluka root`
2. Prepare the folder where to install FLUKA: `cd /usr/local ; sudo mkdir -p FLUKA/INFN/2021.2.9 ; cd FLUKA/INFN/2021.2.9`
3. Move downloaded `.tar.gz` files and extract them: `sudo mv ~/Download/fluka2021.2* . ; sudo su ; tar -xvzf fluka2021.2-data.tar.gz ; tar -xvzf fluka2021.2-linux-gfor64bit-11.2-AA.tar.gz`
4. Become super-user: `sudo su`;
5. Prepare environment for installation: `export FLUPRO=$WPD ; export FLUFOR=gfortran`
6. Compile: `make ; $FLUPRO/flutil/ldpmqmd`
7. Make installation available for the linux group `fluka`: `chmod -R a+r . ; chmod a+x flukahp flukadpm3`
