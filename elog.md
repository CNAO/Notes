# Man Page of elog at CNAO

## User Man

## Admin Man
### Installation on Ubuntu
* download `elog-latest.tar.gz` from the [elog download page](https://elog.psi.ch/elog/download/tar/)
* expand the `*.tar.gz` file: `tar -xzvf elog-x.x.x.tar.gz`;
* before installation, please make sure that the `libssl-dev` package is intalled: `sudo apt-get install libssl-dev`;
* `cd` to the subfolder and run `make` (to compile) and then `make install` (to install executables in appropriate places);
* before running/testing, please create the elog user: `sudo useradd elog --create-home -s /bin/bash ; sudo -u elog /usr/bin/xdg-users-dirs-update`
* you can check the existence of the `elog` user by grepping its info in `/etc/passwd` and `/etc/group`.

### Useful paths and exes/files
| *file* | *path* | *description* | *permissions* |
| --- | --- | --- | --- |
| `elogd` | `/usr/local/sbin` | | |
| `elog` | `/usr/local/bin` | | |
| `elconv` | `/usr/local/bin` | | |
