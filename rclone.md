# Cheat Sheet of `rclone`
This is just a dirty and quick list of useful commands.

## Installation
To install `rclone` from terminal ([ref](https://rclone.org/install/), Linux Installation)
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

## Most common commands
Most of them can be found on the official [webpage](https://rclone.org/docs/) of the package.
* to list files in a path on a remote: `rclone ls remote:path`
* to copy files in `/local/path` to the remote in a specific path: `rclone copy /local/path remote:path`
* to synch `/local/path` to a specific path on the remote: `rclone sync -i /local/path remote:path`
