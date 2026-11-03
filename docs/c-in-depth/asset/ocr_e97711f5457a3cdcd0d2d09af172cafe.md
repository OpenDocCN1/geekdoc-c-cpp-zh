# Exercise

Assume stdio.h is included in all programs.

```
```c
(1) void func(void);
    main()
    {
        printf("Lucknow\\n");
        goto ab;
    }
    void func(void)
    {
        ab:
        printf("Bareilly\\n");
    }
```
```

```
```c
(2) main()
    {
        int i=9;
        if(i==9)
        {
            int i=25;
        }
        printf("i=%d",i);
    }
```
```

```
```c
(3) void func(int a,int b);
    main()
    {
        int x;
        x=func(2,3);
    }
    void func(int a,int b)
    {
        int s;
        s=a+b;
        return;
    }
```
```

```
```c
(4) main()
    {
        int x=5;
        x=func();
        printf("%d\\n",x);
    }
    int func(int a)
    {
        a=a*2;
    }
```
```

```
```c
(5) main()
    {
```
```