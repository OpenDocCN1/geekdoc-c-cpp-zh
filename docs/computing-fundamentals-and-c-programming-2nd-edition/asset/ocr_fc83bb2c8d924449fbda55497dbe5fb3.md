```
```c
printf("\nNow x = %d\n",x);
}
```
```

```
```text
Output

Value of x is 10
10 is stored at addr 4104
10 is stored at addr 4104
10 is stored at addr 4104
4104 is stored at addr 4106
10 is stored at addr 4108
Now x = 25
```
```

**Fig. 13.5** *Accessing a variable through its pointer*

The actions performed by the program are illustrated in Fig. 13.6. The statement ptr = &x assigns the address of x to ptr and y = *ptr assigns the value pointed to by the pointer ptr to y.

![](bbox=[0.21, 0.445, 0.785, 0.86])

**Fig. 13.6** *Illustration of pointer assignments*