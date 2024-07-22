# Cheat Sheet for Installing FLUKA
1. Prepare a `fluka` linux group and add all the concerned users (including `root`): `sudo addgroup fluka; sudo usermod -aG fluka root`
1. Download `.tar.gz` files from the [fluka website](https://www.fluka.org/fluka.php?id=download&sub=packages_ok);
1. Prepare the folder where to install FLUKA: `cd /usr/local ; sudo mkdir -p FLUKA/INFN/2021.2.9 ; cd FLUKA/INFN/2021.2.9`
1. Move downloaded `.tar.gz` files: `sudo mv ~/Downloads/fluka2021.2* . ; sudo su`
1. extract them: `tar -xvzf fluka2021.2-data.tar.gz ; tar -xvzf fluka2021.2-linux-gfor64bit-11.2-AA.tar.gz`
1. Prepare environment for installation: `export FLUPRO=$PWD ; export FLUFOR=gfortran`
1. Compile: `make ; $FLUPRO/flutil/ldpmqmd`
1. Make installation available for the linux group `fluka`: `chmod -R a+r . ; find . -type f -executable -exec chmod a+x {} \;` and then `cd ../../../ ;  chown -R root:fluka FLUKA`

Further notes on the FLUKA installation can be found on the [FLUKA website](http://www.fluka.org/fluka.php?id=ins_run&mm2=3)

All in one go (bash):
```
# bash
export myUserID=<user_ID>
export myUserPass=<user_pass>
export FLUKAver=2024.1
export FLUKAverLong=2024.1.0
export GFORver=11.4
export GLIBCver=2.35

# download stuff
cd Downloads
wget --user ${myUserID} --password ${myUserPass} https://www.fluka.org/packages/fluka${FLUKAver}-linux-gfor64bit-${GFORver}-glibc${GLIBCver}-AA.tar.gz
wget --user ${myUserID} --password ${myUserPass} https://www.fluka.org/packages/fluka${FLUKAver}-data.tar.gz

# create appropriate folder with downloaded material
cd /usr/local
sudo mkdir -p FLUKA/INFN/${FLUKAverLong}
cd FLUKA/INFN/${FLUKAverLong}
sudo mv ~/Downloads/fluka${FLUKAver}*tar.gz .
sudo tar -xvzf fluka${FLUKAver}-linux-gfor64bit-${GFORver}-glibc${GLIBCver}-AA.tar.gz
sudo tar -xvzf fluka${FLUKAver}-data.tar.gz

# prepare for installation
sudo su
export FLUPRO=$PWD
export FLUKA=${FLUPRO}
export FLUFOR=gfortran

# compile
make ; $FLUPRO/flutil/ldpmqmd

# make installation available for the linux group fluka
chmod -R a+r .
find . -type f -executable -exec chmod a+x {} \;
cd ../../../
chown -R root:fluka FLUKA

# clean away package files
cd -
rm fluka${FLUKAver}*tar.gz
```

# Cheat Sheet for Installing FLAIR
1. Download `.tar.gz` files from the [FLAIR website](https://www.fluka.org/flair/download.html);
1. All operations should be done as admin: `sudo su`;
1. Extract downloaded `.tar.gz` files: `tar -xvzf flair-2.3-0cpy3.tgz ; tar -xvzf flair-geoviewer-2.3-0cpy3.tgz`
1. Install `flair`: `cd flair-2.3 ; make install ; cd -`
1. Install `geoviewer`: `cd flair-geoviewer-2.3 ; make ; make install ; cd -` . In case of problems with `python` (e.g. `python: No such file or directory` or `python-config: No such file or directory`), please prepare the appropriate links in `/usr/bin`, e.g. `cd /usr/bin; ln -s python3 python; ln -s python3-config python-config; cd -`
1. Make installation available for the linux group `fluka`: `cd /usr/local/flair ; chmod -R a+r . ; find . -type f -executable -exec chmod a+x {} \;` and then `chown -R root:fluka .`

Further notes on the FLAIR installation can be found on the [FLAIR website](https://www.fluka.org/flair/download.html)

All in one go (bash):
```
# become sudo
sudo su

# set envar variables
export FLAIRver=2.3
export FLAIRverLong=2.3-0epy3

# download stuff
cd Downloads
wget https://www.fluka.org/flair/flair-${FLAIRverLong}.tgz
wget https://www.fluka.org/flair/flair-geoviewer-${FLAIRverLong}.tgz

# extract downloaded stuff
tar -xvzf flair-${FLAIRverLong}.tgz
tar -xvzf flair-geoviewer-${FLAIRverLong}.tgz

# install flair and geoviewer
cd flair-${FLAIRver} ; make install ; cd -
cd flair-geoviewer-${FLAIRver} ; make ; make install ; cd -

# make installation available for the linux group fluka:
cd /usr/local/flair
chmod -R a+r .
find . -type f -executable -exec chmod a+x {} \;
chown -R root:fluka .

# clean away package files
cd -
rm fluka${FLUKAver}*tar.gz
```
