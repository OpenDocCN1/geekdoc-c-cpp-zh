```
static ssize_t my_led_write(struct file file, const char __user buf, size_t count, loff_t offset) char data;

    if (copy_from_user(&data, buf, 1))
        return -EFAULT;
    }
    gpio_set_value(LED_GPIO, data == '1'); // Turn LED on or off return
count;
    }
// other file operations

static struct file_operations fops
    .owner = THIS_MODULE,
    .open = my_led_open,
    .release = my_led_release,
    .write = my_led_write,
};
static int __init my_led_init(void)
    major_number = register_chrdev(0, DEVICE_NAME, &fops); if
(major_number < 0)
        printk(KERN_ALERT "my_led: cannot register character device\n"); return major_number;
    }
    printk(KERN_INFO "my_led: registered with major number %d\n", major_number); return 0;
    }
static void __exit my_led_exit(void)
    unregister_chrdev(major_number, DEVICE_NAME);
    printk(KERN_INFO "my_led: unregistered\n");
}
module_init(my_led_init);
module_exit(my_led_exit);
```

# Key points:

+   - The gpio_request and gpio_direction_output functions are used to configure the GPIO pin as an output.