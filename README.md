# framebuffer driver for st7796

已测试设备：`树莓派5`正常运行

## dts文件编译
```bash
 dtc -I dts -O dtb -o rpi5-st7796s.dtbo rpi5-st7796s.dts

 sudo cp ./rpi5-st7796s.dtbo /boot/firmware/overlays       
```

## 内核模块文件编译
```bash
make clean && make 
sudo make rpi-install   
```

## 添加overlay
根据实际使用的设备，此处提供树莓派的覆盖方法

```
dtoverlay=rpi5-st7796s
```

## 内核版本太新的情况下，会导致在镜像源中无法下载到相应的内核头文件，需要降级内核
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