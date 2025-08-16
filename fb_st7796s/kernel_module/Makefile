obj-m := fb_st7796s.o

PWD := $(shell pwd)

EXTRA_CFLAGS += -Wno-incompatible-pointer-types

# 检测是否为树莓派
ifeq ($(shell uname -m), armv7l)
    KDIR ?= /lib/modules/$(shell uname -r)/build
else ifeq ($(shell uname -m), aarch64)
    KDIR ?= /lib/modules/$(shell uname -r)/build
else
    KDIR ?= /lib/modules/$(shell uname -r)/build
endif

all: default

default:
	make -C $(KDIR) M=$(PWD) modules

install:
	make -C $(KDIR) M=$(PWD) modules_install
	depmod -a

clean:
	make -C $(KDIR) M=$(PWD) clean

# 添加树莓派特定的安装目标
rpi-install: default
	sudo cp fb_st7796s.ko /lib/modules/$(shell uname -r)/kernel/drivers/staging/fbtft/
	sudo depmod -a
	echo "fb_st7796s" | sudo tee -a /etc/modules