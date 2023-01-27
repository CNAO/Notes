# Cheat Sheet of `rclone`
This is just a dirty and quick list of useful commands.
Most of them can be found on the official [webpage](https://rclone.org/docs/) of the package.
* to list files in a path on a remote: `rclone ls remote:path`
* to copy files in `/local/path` to the remote in a specific path: `rclone copy /local/path remote:path`
* to synch `/local/path` to a specific path on the remote: `rclone sync -i /local/path remote:path`
