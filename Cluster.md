# Some useful programs
Nota bene: installation commands are referred to Ubuntu 22.04 LTS
| *name* | *install command* | *comment* |
| --- | --- | --- |
| emacs | `sudo apt-get install emacs` | text file editor |
| meld | `sudo apt-get install meld` | text file editor - useful for comparing text files |
| git | `sudo apt-get install git` | revision tracking system |
| gparted | `sudo apt-get install gparted` | tool to view partitions on filesystem |
| tkdiff | `sudo apt-get install tkdiff` | a tool for diffing ASCII files (includes `tk` and `libtk`) |
| make | `sudo apt-get install make` | Linux utility to compile exes |
| xterm | `sudo apt-get install xterm` | a light version of the Linux terminal |
| htop | `sudo apt-get install htop` | a user friendly interface to linux `top` |

Required by FLUKA:
| *name* | *install command* | *comment* |
| --- | --- | --- |
| gcc | `sudo apt-get install gcc` | gnu `C` compiler (includes `libc`) |
| gfortran | `sudo apt-get install gfortran` | gnu `fortran` compiler |

Required by FLAIR:
| *name* | *install command* | *comment* |
| --- | --- | --- |
| py-dev | `sudo apt-get install python3-dev` | `python3` development module |
| numpy | `sudo apt-get install python3-numpy` | `python3` module for numerical calculus |
| scipy | `sudo apt-get install python3-scipy` | `python3` module for scientific calculus |
| dicom | `sudo apt-get install python3-dicom` | `python3` module for handling dicom images |
| gnuplot | `sudo apt-get install gnuplot` | plotting language |
|  | `sudo apt install libx11-dev tcl-dev tk-dev python3-tk` | various support libs |

All the above in one go:

```sudo apt-get install emacs meld git gparted tkdiff make xterm htop gcc gfortran python3-dev python3-numpy python3-scipy python3-dicom gnuplot libx11-dev tcl-dev tk-dev python3-tk```

This download totals to a bit less than 1 GB.

## Additional Packages
| *name* | *install command* | *comment* |
| --- | --- | --- |
| google chrome | see Notes | web browser |
| openssh | `sudo apt install openssh-server ` | package installed on a machine to make it reachable via `ssh` (see Notes for checks) |

Notes:
* to check that `openssh` is up and running: `sudo service ssh status`
* to install google chrome from terminal:
```
cd ~/Downloads
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo chown -Rv _apt:root ./google-chrome-stable_current_amd64.deb
sudo chmod -Rv 700 ./google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
```

# VMs
## VirtualBox
In order to have your VM visible directly from the router, please change the network settings of the VM when switched off:
1. `Settings -> Network`
2. In the first tab, change from `NAT` to `Bridged Adapter`. Please make sure to select the correct network card (i.e. LAN vs wireless) and under `Advanced` make sure the promiscuous mode to `Allow All`.
