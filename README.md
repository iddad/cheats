
# Windows: synchronize two directories
The easiest way seems to use rsync as it also works on Linux and macOS.
Rsync doesn't exist as a standalone on Windows so we'll use a busybox.

## Install Rsync on Windows
* Download and install `Git Bash`: https://git-scm.com/
* Download additional `rsync` package from the repo: http://repo.msys2.org/msys/x86_64/
* Open the `rsync-{version}.pkg.tar.xz` package with 7Zip and extract the executable `/usr/bin/rsync.exe`
* Copy the executable `rsync.exe` to `C:\Program Files\Git\usr\bin\`
* Test it: open a Git Bash terminal and type `rsync`

## Synchronize two directories
```bash
# Synchronize two directories using rsync
# flags:
#  -v  verbose
#  -r  recursive
#  -a  keeps original time and date
#  -n  simulated mode, does not sync
rsync -vra origin2/ dest/
```
