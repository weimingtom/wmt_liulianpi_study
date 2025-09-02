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

## v3s, mount and umount tf card
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
* umount
```
# df -h
Filesystem                Size      Used Available Use% Mounted on
/dev/root                 9.9M      3.6M      6.4M  36% /
devtmpfs                 26.4M         0     26.4M   0% /dev
tmpfs                    26.9M         0     26.9M   0% /dev/shm
tmpfs                    26.9M     24.0K     26.8M   0% /tmp
tmpfs                    26.9M     16.0K     26.9M   0% /run
/dev/mmcblk0p1           29.1G     64.0K     29.1G   0% /mnt/SDCARD
# umount /dev/mmcblk0p1
umount: can't unmount /mnt/SDCARD: Device or resource busy
# cd
# umount /mnt/SDCARD
```

## v3s, lvgl9_demo
* lvgl9_demo, built with lvgl9_v1.zip (repacked from lvgl9.zip from author of liulianpi) and lvgl9.tar.gz (my mod and build, change CC)
* How to run ? Copy to tf card (formated to FAT32) and insert it into liulianpi (also you can insert it before v3s booting), then run (no need to chmod +x)  
```
# mkdir /mnt/SDCARD
# fdisk -l
# mount /dev/mmcblk0p1 /mnt/SDCARD
# cd /mnt/SDCARD
# ./lvgl9_demo
```
* lvgl9.zip use lvgl/lv_port_linux 2024-08-27 (not sure, but a little large different), see also https://github.com/lvgl/lv_port_linux/tree/b821c2
* lvgl9.zip use lvgl-9.2.2, see also https://github.com/lvgl/lvgl/releases/tag/v9.2.2
* https://bbs.aw-ol.com/topic/303/%E5%93%AA%E5%90%92d1%E5%BC%80%E5%8F%91%E6%9D%BF-lvgl7-%E6%BA%90%E7%A0%81%E4%B8%8B%E8%BD%BD-%E5%B8%A6git%E4%BB%93%E5%BA%93/31?lang=zh-CN
* lv_port_linux_frame_buffer_nezha_d1_hdmi_event3_git.tgz
* https://github.com/weimingtom/wmt_lvgl_study
* https://gitee.com/RCSN/lv_port_linux_frame_buffer_mq_d1s
