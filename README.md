## UID: 005412538

# Hey! I'm Filing Here

This code implements a rudimentary ext2 filesystem. The root directory created should contain a lost+found folder, a hello-world file, and a symlink named hello pointing to the hello-world file.

## Building

```bash
# compile binary
make
```

## Running

```bash
# create the filesystem
./ext2-create
# create mount point and mount filesystem
mkdir mnt && sudo mount -o loop cs111-base.img mnt
# check contents of mounted filesystem
ls -ain mnt
# total 7
#       2 drwxr-xr-x 3    0    0 1024 Jun  5 19:03 .
# 1217593 drwxr-xr-x 3 1000 1000 4096 Jun  5 19:08 ..
#      13 lrw-r--r-- 1 1000 1000   11 Jun  5 19:03 hello -> hello-world
#      12 -rw-r--r-- 1 1000 1000   12 Jun  5 19:03 hello-world
#      11 drwxr-xr-x 2    0    0 1024 Jun  5 19:03 lost+found
```
The output from `ls -ain` should be exactly the same, spare the `..` directory details (this will be machine specific as it's not apart of the mounted fs).

## Testing

```bash
# check the filesystem metadata
dumpe2fs cs111-base.img
# check filesystem integrity
fsck.ext2 cs111-base.img
```

## Cleaning up

```bash
# clean build files and resulting binary
make clean
# unmount the filesystem and remove the temporary directory
sudo umount mnt && rm -r mnt
```
