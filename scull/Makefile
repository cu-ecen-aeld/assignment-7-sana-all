# Comment/uncomment the following line to disable/enable debugging
#DEBUG = y


# Add your debugging flag (or not) to CFLAGS
ifeq ($(DEBUG),y)
  DEBFLAGS = -O -g -DSCULL_DEBUG # "-O" is needed to expand inlines
else
  DEBFLAGS = -O2
endif

LDDINC=$(PWD)/../include

EXTRA_CFLAGS += $(DEBFLAGS)
EXTRA_CFLAGS += -I$(LDDINC)

ifneq ($(KERNELRELEASE),)
# call from kernel build system

scull-objs := main.o pipe.o access.o

obj-m	:= scull.o

else

# The kernel source tree must be passed in from the environment
# (Yocto recipe sets KERNEL_SRC). Do not default to host /lib/modules.
PWD       := $(shell pwd)

modules:
    $(MAKE) -C $(KERNEL_SRC) M=$(PWD) modules

modules_install:
    $(MAKE) -C $(KERNEL_SRC) M=$(PWD) modules_install

clean:
    $(MAKE) -C $(KERNEL_SRC) M=$(PWD) clean

endif

