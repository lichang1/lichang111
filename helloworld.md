1.helloworld
#include <linux/init.h>
#include <linux/module.h>
#include <linux/moduleparam.h>
 
MODULE_LICENSE("Dual BSD/GPL");
 
static int hello_init(void)
{
	printk(KERN_ALERT"Hello!\n");
	return 0;
}
 
static void hello_exit(void)
{
	printk(KERN_ALERT"Goodbye!\n");
}
 
module_init(hello_init);
module_exit(hello_exit);


2.makefile

KERN_DIR = /lib/modules/$(shell uname -r)/build
 
all:
	make -C $(KERN_DIR) M=`pwd` modules
 
clean:
	make -C $(KERN_DIR) M=$(shell pwd) modules clean
	rm -rf modules.order
 
obj-m := hello.o
