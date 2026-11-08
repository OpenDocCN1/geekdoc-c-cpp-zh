```
```c
#include <linux/module.h> /* Specifically, a module */
int init_module(void)
{
    printk(KERN_INFO "Hello, world - in start\n");
    return 0;
}
```
```

Following is the code for stop.c:

```
```c
/* stop.c - Illustration of multi filed modules */

#include <linux/kernel.h> /* we're doing kernel work */
#include <linux/module.h> /* Specifically, a module */
void cleanup_module()
{
    printk(KERN_INFO "Good Bye - in stop.\n");
    return 0;
}
```
```

The start.c file contains the definition of the init_module() function; whereas, the stop.c file contains the definition of the cleanup_module() function.

Now, we need to compile both the files and generate the .ko file to load the kernel module. Till now, we have learned to generate the .ko file by compiling a single source file by using the make command. Therefore, a question arises that will there be two different kernel modules for this example; one for start.c and the other for stop.c. The answer to this question is no, as a single kernel module will be generated after compiling the start.c and stop.c files. The Makefile for this example will contain the name for both the programs, as shown as follows:

```
```makefile
obj-m += startstop.o
startstop-objs := start.o stop.o
all:
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
clean:
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```
```

Executing the Makefile by using the make command generates a kernel module called startstop.ko, which can be loaded and unloaded from the kernel using the insmod and rmmod commands, respectively.

After having an idea on how kernel modules are written, let's discuss the primary differences between a kernel module and a C user-space program.

# ### Kernel Modules vs. C User-Space Programs

A C user-space program begins with a main() function, executes a set of instructions, and terminates the execution upon completion of those instructions. On the other hand, a kernel module always begins with the startup function, which is either init_module or the function that is specified within the module_init macro. The startup function, once invoked as the kernel module loads, sets up the environment in the kernel to run the module's functions whenever they are required.

To end the execution of a C user-space program, nothing special needs to be done; however, to unload a kernel module, we should always call the cleanup function, which is either cleanup_module or the function that is specified with the module_exit call. The cleanup function is the exit point for every kernel module, where it unregisters all the functionalities that the entry function had once registered. Every Linux kernel module must have an entry function and an exit function.