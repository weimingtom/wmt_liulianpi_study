# wmt_liulianpi_study
My LiuLianPi study

## ref
* https://github.com/weimingtom/wmt_mt7688_study
* https://github.com/weimingtom/wmt_lvgl_study
* v3s: http://doc.liulianpi.cn/web/#/7
* f1c100s: http://doc.liulianpi.cn/web/#/5

## v3s, clear screen, 480x272, 1920 == 480 * 4
```
# fbset

mode "480x272-0"
        # D: 0.000 MHz, H: 0.000 kHz, V: 0.000 Hz
        geometry 480 272 480 272 32
        timings 0 0 0 0 0 0 0
        accel true
        rgba 8/16,8/8,8/0,0/0
endmode

# cat /bin/busybox > /dev/fb0
# dd if=/dev/zero of=/dev/fb0 bs=1920 count=272
```

## v3s, mount
```
# mkdir /mnt/SDCARD
# [ 1367.283998] mmc0: card 0001 removed
[ 1465.929778] mmc0: host does not support reading read-only switch, assuming write-enable
[ 1465.939855] mmc0: new high speed SDHC card at address 0001
[ 1465.947700] mmcblk0: mmc0:0001 SD 29.1 GiB
[ 1465.953666]  mmcblk0: p1

# fdisk -l
Disk /dev/mmcblk0: 29 GB, 31266439168 bytes, 61067264 sectors
3801 cylinders, 255 heads, 63 sectors/track
Units: sectors of 1 * 512 = 512 bytes

Device       Boot StartCHS    EndCHS        StartLBA     EndLBA    Sectors  Size Id Type
/dev/mmcblk0p1    0,0,2       1023,254,63          1   61067262   61067262 29.1G  c Win95 FAT32 (LBA)
# mount /dev/mmcblk0p1 /mnt/SDCARD
# cd /mnt/SDCARD
# ls
System Volume Information
```
* If echo: mount: mounting /dev/mmcblk0p1 on /mnt/SDCARD failed: Invalid argument
* Please format it as FAT32
