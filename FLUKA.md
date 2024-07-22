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
2. All operations should be done as admin: `sudo su`;
3. Extract downloaded `.tar.gz` files: `tar -xvzf flair-2.3-0cpy3.tgz ; tar -xvzf flair-geoviewer-2.3-0cpy3.tgz`
4. Install `flair`: `cd flair-2.3 ; make install ; cd -`
5. Install `geoviewer`: `cd flair-geoviewer-2.3 ; make ; make install ; cd -` . In case of problems with `python` (e.g. `python: No such file or directory` or `python-config: No such file or directory`), please prepare the appropriate links in `/usr/bin`, e.g. `cd /usr/bin; ln -s python3 python; ln -s python3-config python-config; cd -`
7. Make installation available for the linux group `fluka`: `cd /usr/local/flair ; chmod -R a+r . ; find . -type f -executable -exec chmod a+x {} \;` and then `chown -R root:fluka .`

Further notes on the FLAIR installation can be found on the [FLAIR website](https://www.fluka.org/flair/download.html)
