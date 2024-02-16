These are some technical notes regarding the installation of `Xsuite` on CNAO computers.

# Installation 
These instructions apply to the installation of `Xsuite` on `Ubuntu 20.04 LTS` on a `VirtualBox` VM (v6.1.40 r154048).
Please note that the CNAO IT service won't allow you to the end of the installation process; therefore, please connect your pc to the internet via an hotspot.
One of the best places where to locate your mobile phone field is saletta ristoro (1st floor).
The HotSpot field should be strong enough to be seen by your computer in the offices nearby.

Installation steps:
* prior to installation, please install Miniforge, as suggested on the [Xsuite user manual](https://xsuite.readthedocs.io/en/latest/installation.html#miniforge);
* please install all the packages reported in the Xsuite user's guide. The developer [installation](https://xsuite.readthedocs.io/en/latest/installation.html#developer-installation) allows to edit the source code and to deploy the modifications straight away. Please keep in mind to fork the mentioned packages, such that in case of actual patches, they can be given to the developers via usual dev scheme of `github.com`;
* in case of troubles with the https ceritificates, please follow these steps:
	* add the correct CA certificate ([credits](https://stackoverflow.com/questions/21181231/server-certificate-verification-failed-cafile-etc-ssl-certs-ca-certificates-c)):
	1. find the correct certificate: `echo -n | openssl s_client -showcerts -connect github.com:443 2>/dev/null  | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'`
	2. find the correct file where to copy-paste the certificate: `curl-config --ca` (you may need to install this package - Ubuntu will prompt you on how to do that);
	3. copy-paste the certificate at the end of the file found in the previous step (you may need to `sudo`);
	* add `files.pythonhosted.org` among the trusted sources ([credits](https://stackoverflow.com/questions/25981703/pip-install-fails-with-connection-error-ssl-certificate-verify-failed-certi)): `pip config set global.trusted-host "files.pythonhosted.org" --trusted-host=files.pythonhosted.org`;
* in case of troubles with package hases (e.g. `ERROR: THESE PACKAGES DO NOT MATCH THE HASHES FROM THE REQUIREMENTS FILE. etc...`:
	* clean the `pip install` cache ([credits](https://stackoverflow.com/questions/40183108/python-packages-hash-not-matching-whilst-installing-using-pip)): `pip cache purge`;
	
