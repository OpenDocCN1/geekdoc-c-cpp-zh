# Chapter 5. Threads and Shared Memory

![](bbox=[0.296, 0.159, 0.725, 0.375])

Figure 5.3: Illustration of how vm areas are accessed.

# VM areas in the Linux kernel

VM (virtual memory) areas¹³ are data structures maintained by the kernel for each process that specify which virtual addresses the program may legally generate.

The definition of sys_getpid(), which implements the getpid() system call, is found in kernel/timer.c in the source tree of Linux version 3.6. This system call is modified to access the vm area that contains the user mode stack. The following code is inserted into sys_getpid():

```
if((300<=dv_print_flag)&&(dv_print_flag<400)){
    struct vm_area_struct *dv_vmptr
    = find_vma(current->mm, current->mm->start_stack);
    printk(KERN_ALERT "vm_start = %1lx \n",
        dv_vmptr->vm_start);
    printk(KERN_ALERT "vm_end = %1lx \n",
        dv_vmptr->vm_end);
}
```

The print flag, which is set using the system call of section 5.4.1, is used to turn the print statements on or off.

> ¹³See Bovet and Cesati (2005).