+   - alloc_chrdev_region allocates a major number for the device and registers the device name.
+   - cdev_alloc allocates a cdev structure.
+   - cdev_init initializes the cdev structure with file operations.
+   - cdev_add adds the cdev to the system.

# Unregistration

```
static void __exit my_device_exit(void) {
    // Get the cdev structure
    struct cdev *my_cdev = cdev_get(MKDEV(my_major, 0));

    // Delete the cdev
    cdev_del(my_cdev);

    // Unregister the character device
    unregister_chrdev_region(my_major, 1);
}
```

+   - cdev_get retrieves the cdev structure.
+   - cdev_del deletes the cdev.
+   - unregister_chrdev_region unregisters the character device.

# Block Device Registration and Unregistration

Block devices are used for devices that transfer data in fixed-size blocks.