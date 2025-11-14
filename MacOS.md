# Mapping Linux commands/tasks to MacOS terminal line commands

1. install brew: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"` (from [brew.sh](https://brew.sh/));
2. whichever linux package you need, replace `apt-get install` with `brew install`;
3. add a group (eg `fluka`): `sudo dseditgroup -o create fluka` (from [serverfault.com](https://serverfault.com/questions/131942/how-do-i-add-a-group-in-mac-os-x-10-6));
4. add a user (eg `pippo`): to a group (eg `fluka`): `sudo dseditgroup -o edit -a pippo -t user fluka` (from [superuser.com](https://superuser.com/questions/214004/how-to-add-user-to-a-group-from-mac-os-x-command-line));
5. change attributes to exe files: `find . -type f -perm +111 -exec chmod a+x {} \;` (from [apple.stackexhange.com](https://apple.stackexchange.com/questions/116367/find-all-executable-files-within-a-folder-in-terminal));
