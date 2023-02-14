# Notes about environment in VMs
This file summarises some infos concerning our VM Linux machines.

## Ubuntu 22.04 LTS on Win machine WS0040
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
* create a dedicated folder on `DATA`, e.g.: `drwxrwxr-x 2 amereghe amereghe  4096 gen 20 15:20 amereghe/`

### Environment variables
```
# .bashrc
# terminal line behavior:
# - do not escape $ when tabbing:
shopt -s direxpand
# use local numeric interpretation as default C
export LC_NUMERIC=C
# env vars for FLUKA
export FLUPRO=/usr/local/FLUKA/INFN/2021.2.8
export FLUKA=/usr/local/FLUKA/INFN/2021.2.8
export FLUFOR=gfortran
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
### Useful paths
| *VM Path* | *Description* | 
| --- | --- |
| `/home/<username>` | home folder of each user. Desktop is found at `/home/<username>/Desktop` |
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
* create a dedicated folder on `DATA`, e.g.: `drwxrwxr-x 2 amereghe amereghe  4096 gen 20 15:20 amereghe/`

### Environment variables
```
# .bashrc
# env vars for FLUKA
export FLUPRO=/usr/local/FLUKA/INFN/2021.2.9
export FLUKA=${FLUPRO}
export FLUFOR=gfortran
```

### File System Table
```
# Use shared folders between VMWare guest and host
.host:/         /mnt/hgfs    fuse.vmhgfs-fuse    defaults,allow_other     0    0
# permanently mount DATA readable and writeable by every user
/dev/sda4	/mnt/DATA	ext4	defaults	0	0
```

# Some useful admin commands (Ubuntu)
* add new group `$ sudo addgroup <myGroupName>`  (from [link](https://subscription.packtpub.com/book/networking-&-servers/9781785883064/1/ch01lvl1sec12/creating-a-group));
* add existing user to existing group: `$ sudo usermod -aG <myGroupName> <myUserName>` (from [link](https://www.howtogeek.com/50787/add-a-user-to-a-group-or-second-group-on-linux/));
* mount shared folders (VMware):
`sudo vmhgfs-fuse .host:/ /mnt/hgfs/ -o allow_other -o uid=1000` (from [link](https://askubuntu.com/questions/29284/how-do-i-mount-shared-folders-in-ubuntu-using-vmware-tools))
* to enter bios: press `F2`;

# Some useful programs
Nota bene: installation commands are referred to Ubuntu 22.04 LTS
| *name* | *install command* | *comment* |
| --- | --- | --- |
| google chrome | see Notes | web browser |
| emacs | `sudo apt-get install emacs` | text file editor |
| meld | `sudo apt-get install meld` | text file editor - useful for comparing text files |
| git | `sudo apt-get install git` | revision tracking system |
| gparted | `sudo apt-get install gparted` | tool to partition filesystem |
| tkdiff | `sudo apt-get install tkdiff` | a tool for diffing ASCII files (includes `tk` and `libtk`) |
| make | `sudo apt-get install make` | Linux utility to compile exes |
| xterm | `sudo apt-get install xterm` | a light version of the Linux terminal |
| htop | `sudo apt-get install htop` | a user friendly interface to linux `top` |
| rclone | see Notes | command-line interface for synching files against eg Google Drive |

Required by FLUKA:
| *name* | *install command* | *comment* |
| --- | --- | --- |
| gcc | `sudo apt-get install gcc` | gnu `C` compiler (includes `libc`) |
| gfortran | `sudo apt-get install gfortran` | gnu `fortran` compiler |

Required by FLAIR:
| *name* | *install command* | *comment* |
| --- | --- | --- |
| numpy | `sudo apt-get install python3-numpy` | `python3` module for numerical calculus |
| scipy | `sudo apt-get install python3-scipy` | `python3` module for scientific calculus |
| dicom | `sudo apt-get install python3-dicom` | `python3` module for handling dicom images |
| gnuplot | `sudo apt-get install gnuplot` | plotting language |
|  | `sudo apt install libx11-dev tcl-dev tk-dev python3-tk` | various support libs |

Notes:
* to install google chrome from terminal:
```
cd ~/Downloads
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo chown -Rv _apt:root ./google-chrome-stable_current_amd64.deb
sudo chmod -Rv 700 ./google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
```
* to install `rclone` from terminal ([ref](https://rclone.org/install/), Linux Installation)
```
# Fetch and unpack
wget https://downloads.rclone.org/rclone-current-linux-amd64.zip
unzip rclone-current-linux-amd64.zip
cd rclone-*-linux-amd64
# Copy binary file
sudo cp rclone /usr/bin/
sudo chown root:root /usr/bin/rclone
sudo chmod 755 /usr/bin/rclone
# Install manpage
sudo mkdir -p /usr/local/share/man/man1
sudo cp rclone.1 /usr/local/share/man/man1/
sudo mandb
```

# Cheat Sheet for Installing FLUKA
1. Prepare a `fluka` linux group and add all the concerned users (including `root`): `sudo addgroup fluka; sudo usermod -aG fluka root`
2. Download `.tar.gz` files from the [fluka website](https://www.fluka.org/fluka.php?id=download&sub=packages_ok); 
3. Prepare the folder where to install FLUKA: `cd /usr/local ; sudo mkdir -p FLUKA/INFN/2021.2.9 ; cd FLUKA/INFN/2021.2.9`
4. Move downloaded `.tar.gz` files: `sudo mv ~/Downloads/fluka2021.2* . ; sudo su`
5. extract them: `tar -xvzf fluka2021.2-data.tar.gz ; tar -xvzf fluka2021.2-linux-gfor64bit-11.2-AA.tar.gz`
6. Prepare environment for installation: `export FLUPRO=$PWD ; export FLUFOR=gfortran`
7. Compile: `make ; $FLUPRO/flutil/ldpmqmd`
8. Make installation available for the linux group `fluka`: `chmod -R a+r . ; find . -type f -executable -exec chmod a+x {} \;` and then `cd ../../../ ;  chown -R root:fluka FLUKA`

Further notes on the FLUKA installation can be found on the [FLUKA website](http://www.fluka.org/fluka.php?id=ins_run&mm2=3)

# Cheat Sheet for Installing FLAIR
1. Download `.tar.gz` files from the [FLAIR website](https://www.fluka.org/flair/download.html); 
2. Extract downloaded `.tar.gz` files: `sudo su ; tar -xvzf flair-2.3-0cpy3.tgz ; tar -xvzf flair-geoviewer-2.3-0cpy3.tgz`
4. Install `flair`: `cd flair-2.3 ; make install ; cd -`
5. Install `geoviewer`: `cd flair-geoviewer-2.3 ; make ; make install ; cd -`
8. Make installation available for the linux group `fluka`: `cd /usr/local/flair ; chmod -R a+r . ; find . -type f -executable -exec chmod a+x {} \;` and then `chown -R root:fluka .`

Further notes on the FLAIR installation can be found on the [FLAIR website](https://www.fluka.org/flair/download.html)
