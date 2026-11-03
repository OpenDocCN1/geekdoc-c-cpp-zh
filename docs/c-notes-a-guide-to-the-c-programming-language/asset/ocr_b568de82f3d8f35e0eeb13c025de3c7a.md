# 6.6 Exit

The exit function

```
int exit(int code);
```

terminates the current process and delivers control to the process originally activating this process. The exit never returns. The argument code may or may not be used depending strongly on the operating system.