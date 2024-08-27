# Linux Cluster
The linux cluster is simply a pool of machines for crunching jobs; jobs are managed by the [HTCondor](https://htcondor.readthedocs.io/en/latest/users-manual/index.html) batch system.

The users are supposed only to submit jobs from their laptops (either native linux machines or VMs) and retrieve results; analysis and input preparation should be performed on their own laptops.

The cluser is currently on a local network with neither external access to internet nor any DNS service: communication between machines takes place simply by IP addresses.
In order for the user to manage jobs, they have to add the sched address explicitly in all the commands.
For the ease of the users, linux aliases can be set (please see below).

# Some useful programs
The following is a list of useful programs to be installed on both the cluster nodes and user's laptops.
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
Any CNAO user willing to run simulations on the cluster is supposed to set up a VM because of CNAO IT rules.
Then, the VM can be connected via WiFi to the cluster.
It is also possible to keep the laptop regularly connected via LAN cable to the network.

## VirtualBox
In order to have your VM visible directly by the router, please change the network settings of the VM (better to set this up before switching on the VM):
1. `Settings -> Network`;
2. In the first tab (`Adapter 1`), change from `NAT` to `Bridged Adapter`. Please make sure to select the correct network card (i.e. LAN vs wireless) and under `Advanced` make sure the promiscuous mode to `Allow All`;

If the user wants also to have regular access to the internet via LAN, the respective settings must be edited:
1. `Settings -> Network`;
2. In the second tab (`Adapter 2`), enable the network card, keep the connection as `NAT`. Please make sure to select the correct network card (e.g. PCnet-FAST III) and under `Advanced` make sure the promiscuous mode to `Allow All`.

# New Users
If you want to add a new user to the HTCondor cluster, some operations must be performed on the cluster itself and on the laptop from which the user wants to submit jobs.

## Operations to be performed on the cluster
1. ADMIN: add a user (no need for admin rights) to each cluster machine. The user name on the cluster machines *must* match that of the user on their own laptop;
2. USER: `ssh` on the cluster AP machine and fetch an HTCondor IDToken for the remote access of the user: `condor_token_fetch -token name_of_laptop` (see the [HTCondor man page](https://htcondor.readthedocs.io/en/latest/users-manual/submitting-a-remote-job.html));

## Operations to be performed on the laptop of the user
1. copy the newly created token file to the appropriate folder on the laptop. The token is found in `~/.condor/tokens.d/` on the cluster AP machine, and should be copied to the same path on the laptop of the user;
2. create appropriate linux aliases to run htcondor commands (for managing jobs) pointing to the cluster `schedd`;
3. copy the file `51-run-as-user.conf` (provided by the admin) in the folder `/etc/condor/config.d` and restart condor (e.g. by typing `systemctl restart condor` on terminal). For both operations, root permissions are needed.

The following is an example of list of aliases to be set up in order to reach the schedd via IP/port (code for `~/.bashrc`):
```
# HTCONDOR remote submission
my_condor_schedd="\"<192.168.abc.xyz:1234?addrs=192.168.abc.xyz-1234&alias=__MYWONDERFULCLUSTERAP__&noUDP&sock=schedd_abcd_1234>\""
alias my_condor_ssh_to_job="condor_ssh_to_job -name ${my_condor_schedd}"
alias my_condor_q="condor_q -global"
alias my_condor_rm="condor_rm -addr ${my_condor_schedd}"
alias my_condor_submit="condor_submit -addr ${my_condor_schedd}"
alias my_condor_transfer_data="condor_transfer_data -addr ${my_condor_schedd}"
```
The actual schedd name/address can be found issueing the following command in a terminal on the laptop of the user: `condor_status -schedd -l | grep MyAddress`;
