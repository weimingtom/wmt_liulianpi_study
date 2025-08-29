# wmt_liulianpi_study
My LiuLianPi study

## ref
* https://github.com/weimingtom/wmt_mt7688_study
* https://github.com/weimingtom/wmt_lvgl_study
* v3s: http://doc.liulianpi.cn/web/#/7
* f1c100s: http://doc.liulianpi.cn/web/#/5

## v3s, clear screen, 480x272, 1920 == 480 * 4
```
cat /bin/busybox > /dev/fb0
dd if=/dev/zero of=/dev/fb0 bs=1920 count=272
```
