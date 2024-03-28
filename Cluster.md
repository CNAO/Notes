# Additional Packages
| *name* | *install command* | *comment* |
| --- | --- | --- |
| openssh | `sudo apt install openssh-server ` | package installed on a machine to make it reachable via `ssh` |

To check that `openssh` is up and running: `sudo service ssh status`

# VMs
## VirtualBox
In order to have your VM visible directly from the router, please change the network settings of the VM when switched off:
1. `Settings -> Network`
2. In the first tab, change from `NAT` to `Bridged Adapter`. Please make sure to select the correct network card (i.e. LAN vs wireless) and under `Advanced` make sure the promiscuous mode to `Allow All`.
