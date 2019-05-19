
## Linux: split a large file into chunks

```
# Split
split -b 500000k 'My video.mpg' video

# Bring parts together:
cat video.?? > 'My video.mpg'
```

## Rename a bunch of screenshots to an ordered list
Rename a bunch of files using a prefix and an index. Here a list of VLC snapshots taken from a GOPRO recording, I want my snapshots to be renamed GOPR1221-`0001`.png, GOPR1221-`0002`.png, ...)
```
i=1; for file in vlcsnap-2016-12-13-*.png; do NEW_FILE_NAME=$(printf "GOPR1221-%04d.png" "$i"); mv "$file" "$NEW_FILE_NAME"; let i=i+1; done
```

## Create an SSH private/public key for auto authentication
```
cd ~
mkdir .ssh
cd .ssh
# -P : protect your key using your password here, leave it empty for no password
ssh-keygen -b 1024 -t rsa -f id_rsa -P ""
```

## MacOS: convert pllist file from binary to xml.
```
plutil -convert xml1 file.plist
```

## ffmpeg

### Cut / Extract a part of a MP4 video or MP3 audio file
Set `-vcodec copy` and `-acodec copy` to avoid reencoding (keep it fast, same quality).
```
# -i   input file (the large one)
# -ss  start time
# -t   duration
ffmpeg -i GOPR0678.MP4  -ss 00:00:00.0 -t 00:01:55.0 -vcodec copy -acodec copy OUTPUT_FILE.MP4
```

### Extract the music from a video file
Example here with a MKV file containing a MP3 audio track.
```
# Extract 43 seconds of audio, starting at 2min53s.
ffmpeg -i MY_VIDEO.x265.HEVC-QC.mkv -f mp3 -vn -ss 00:02:53 -t 00:00:43 Main-theme.mp3
```

## macOS and DMG image files

### Check DMG file encryption
```
hdiutil isencrypted file.dmg
hdiutil imageinfo file.dmg
```

### Resize a (protected) DMG file:
```
# Here '80m'
hdiutil resize -size 80m test-encrypt.dmg
```

## Windows: synchronize two directories
The easiest way seems to use rsync as it also works on Linux and macOS.
Rsync doesn't exist as a standalone on Windows so we'll use a busybox.

### Install Rsync on Windows
* Download and install `Git Bash`: https://git-scm.com/
* Download additional `rsync` package from the repo: http://repo.msys2.org/msys/x86_64/
* Open the `rsync-{version}.pkg.tar.xz` package with 7Zip and extract the executable `/usr/bin/rsync.exe`
* Copy the executable `rsync.exe` to `C:\Program Files\Git\usr\bin\`
* Test it: open a Git Bash terminal and type `rsync`

### Synchronize two directories
```bash
# Synchronize two directories using rsync
# flags:
#  -v  verbose
#  -r  recursive
#  -a  keeps original time and date
#  -n  simulated mode, does not sync
rsync -vra origin2/ dest/
```
