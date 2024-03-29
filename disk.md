### Kernel Supported Filesystems
```shell
# nodev indicates that the filesystem in question is not a physical filesystem that needs a block device to live on, but rather a virtual filesystem that is backed by something other than a block device.
cat /proc/filesystems

ll /lib/modules/$(uname -r)/kernel/fs
```


### CHS

The CHS values in the actual partition table have pretty restrictive maximum values:

- the cylinders field is just 10 bits wide (= values 0-1023)
- the heads field is 8 bits wide (= values 0-255)
- the sectors field is 6 bits wide (= values 0-63)

```shell
> file armv7.img
armv7.img: DOS/MBR boot sector; 
  partition 1 : ID=0xc, active, start-CHS (0x2,10,9), end-CHS (0xc,60,48), startsector 32768, 163840 sectors; 
  partition 2 : ID=0xa9, start-CHS (0xc,60,49), end-CHS (0x94,141,57), startsector 196608, 2189952 sectors
```

### MBR


### Raspberry Pi

An overview of the files on the /boot/firmware partition (the 1st partition
on the SD card) used by the Ubuntu boot process (roughly in order) is as
follows:

* bootcode.bin   - this is the second stage bootloader loaded by all pis with
                   the exception of the pi4 (where this is replaced by flash
                   memory)
* config.txt     - the first configuration file read by the boot process
* syscfg.txt     - the file in which system modified configuration will be
                   placed, included by config.txt
* usercfg.txt    - the file in which user modified configuration should be
                   placed, included by config.txt
* start*.elf     - the third stage bootloader, which handles device-tree
                   modification and which loads...
* uboot*.bin     - various u-boot binaries for different pi platforms; these
                   are launched as the "kernel" by config.txt
* boot.scr       - the boot script executed by uboot*.bin which in turn
                   loads...
* vmlinuz        - the Linux kernel, executed by boot.scr
* initrd.img     - the initramfs, executed by boot.scr
* meta-data      - meta-data for cloud-init; usually just contains the
                   instance id
* network-config - network configuration for cloud-init; edit this to set up
                   wifi access points and other networking settings
* user-data      - user-data for cloud-init; edit this to configure initial
                   users, SSH keys, packages, etc.


### NetBSD
fdisk partition type:
boot partition: FAT32 (c)

NetBSD: a9

fdisk partition table for uSD/Raspberry Pi:

```shell
Disk /dev/sdc: 14.86 GiB, 15931539456 bytes, 31116288 sectors
Disk model: STORAGE DEVICE
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

Device     Boot  Start     End Sectors Size Id Type
/dev/sdc1  *     32768  196607  163840  80M  c W95 FAT32 (LBA)
/dev/sdc2       196608 2386559 2189952   1G a9 NetBSD
```


http://www.netbsd.org/docs/guide/en/chap-inst.html#fig-part
```shell
ubuntu@p0:~$ sudo fdisk -l /dev/sdc2
Disk /dev/sdc2: 14.76 GiB, 15830876160 bytes, 30919680 sectors
Geometry: 64 heads, 32 sectors/track, 1156 cylinders
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: bsd

Slice  Start      End  Sectors  Size Type     Fsize Bsize Cpg
a     196608 31116287 30919680 14.8G 4.2BSD       0     0   0
c          0 31116287 31116288 14.9G unused       0     0   0
d          0 31116287 31116288 14.9G unused       0     0   0
e      32768   196607   163840   80M MS-DOS       0     0   0
```


### Mount an img

```shell
$ sudo fdisk -lu ./armv7.img
Disk ./armv7.img: 1.14 GiB, 1221918720 bytes, 2386560 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

Device       Boot  Start     End Sectors Size Id Type
./armv7.img1 *     32768  196607  163840  80M  c W95 FAT32 (LBA)
./armv7.img2      196608 2386559 2189952   1G a9 NetBSD

$ bc
512 * 196608
100663296
quit

$ sudo mount -t auto -o loop,offset=100663296 armv7.img /mnt/
mount: /mnt: wrong fs type, bad option, bad superblock on /dev/loop8, missing codepage or helper program, or other error.

$ sudo udisksctl loop-setup --file armv7.img
Mapped file armv7.img as /dev/loop8.

$ sudo losetup -l | grep arm
NAME        SIZELIMIT OFFSET AUTOCLEAR RO BACK-FILE                                                               DIO LOG-SEC
/dev/loop8          0      0         0  0 /data/nfs-00690130-9d3d-4d47-84be-568dca383e21/pub/rpi/netbsd/armv7.img   0     512


$ sudo mount /dev/loop8p1 /mnt/

$ mount | grep mnt
/dev/loop8p1 on /mnt type vfat (rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=ascii,shortname=mixed,errors=remount-ro)

$ sudo umount /dev/loop8p1

$ sudo mount /dev/loop8p2 /mnt/
mount: /mnt: wrong fs type, bad option, bad superblock on /dev/loop8p2, missing codepage or helper program, or other error.

$ sudo fdisk -l /dev/loop8p2
Disk /dev/loop8p2: 1.5 GiB, 1121255424 bytes, 2189952 sectors
Geometry: 64 heads, 32 sectors/track, 1165 cylinders
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: bsd

Slice  Start     End Sectors  Size Type     Fsize Bsize Cpg
a     196608 2386559 2189952    1G 4.2BSD       0     0   0
c          0 2386559 2386560  1.1G unused       0     0   0
e      32768  196607  163840   80M MS-DOS       0     0   0

Partition table entries are not in disk order.
```
