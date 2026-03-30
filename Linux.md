# Cheat sheet with some useful linux commands
* add new group `$ sudo addgroup <myGroupName>`  (from [link](https://subscription.packtpub.com/book/networking-&-servers/9781785883064/1/ch01lvl1sec12/creating-a-group));
* add existing user to existing group: `$ sudo usermod -aG <myGroupName> <myUserName>` (from [link](https://www.howtogeek.com/50787/add-a-user-to-a-group-or-second-group-on-linux/));
* combine `.pdf` files: `gs -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=output.pdf -dBATCH <file1>.pdf <file2>.pdf <file3>.pdf`

# Creation of Core Dump Files for Debugging
In ubuntu, core dump files are not written to disk by default. To activate this option (Ubuntu 20.04 LTS) in the window where to run debugging:
* get current limits (as a record): `ulimit -a`
* set limits to infinite: `ulimit -c unlimited`
* activate core dumping: `sudo systemctl enable apport.service`

Core dump files are then found in: `/var/lib/apport/coredump`.
If core dumps cannot be found in the above path, you can search for them with the following command (searches for files with size >100MB):
`sudo find / -type f -name "core*" -size +100M 2>/dev/null`

Once done, you can restore defaults:
* de-activate core dumping: `sudo systemctl disable apport.service`
* set limits to zero: `ulimit -c 0`

This procedure is quite dangerous, as other processes can thus start writing core dump files. Hence, use the procedure just for the time needed.
