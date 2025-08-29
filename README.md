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
