```bash
 dtc -I dts -O dtb -o rpi5-st7796s.dtbo rpi5-st7796s.dts
```

```bash
zhouzihao@zhouzihao ~ ❯ sudo apt install linux-image-6.12.34+rpt-rpi-v8

zhouzihao@zhouzihao ~ ❯ sudo update-initramfs -u

zhouzihao@zhouzihao ~ ❯ sudo cp /boot/vmlinuz-6.12.34+rpt-rpi-v8 /boot/firmware/
sudo cp /boot/initrd.img-6.12.34+rpt-rpi-v8 /boot/firmware/

sudo chmod 755 /boot/firmware/vmlinuz-6.12.34+rpt-rpi-v8
sudo chmod 755 /boot/firmware/initrd.img-6.12.34+rpt-rpi-v8

编辑/boot/firmware/config.txt
末尾加入
kernel=vmlinuz-6.12.34+rpt-rpi-v8
initramfs initrd.img-6.12.34+rpt-rpi-v8 followkernel

sudo reboot
```

```bash
dtoverlay=rpi5-st7796s
make clean && make 
sudo make rpi-install   
```

覆盖层可选参数参考：

```bash
#dtoverlay=fbtft,spi0-0,st7789v,fps=60,speed=50000000,dc_pin=5,reset_pin=6,cs_pin=8,rotate=90
```
