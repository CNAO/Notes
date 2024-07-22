# Cheat sheet with some useful linux commands
* add new group `$ sudo addgroup <myGroupName>`  (from [link](https://subscription.packtpub.com/book/networking-&-servers/9781785883064/1/ch01lvl1sec12/creating-a-group));
* add existing user to existing group: `$ sudo usermod -aG <myGroupName> <myUserName>` (from [link](https://www.howtogeek.com/50787/add-a-user-to-a-group-or-second-group-on-linux/));
* combine `.pdf` files: `gs -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=output.pdf -dBATCH <file1>.pdf <file2>.pdf <file3>.pdf`
