


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
