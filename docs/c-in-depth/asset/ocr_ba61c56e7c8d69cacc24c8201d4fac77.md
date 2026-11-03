```
~~~c
    INT a=2,*p=&a;
    printf("%d %d\n",a,*p);
}
~~~
```

```
~~~c
(14)#define Y 10
main()
{
    #if X || Y && Z
        printf("Sea in Depth\n");
    #else
        printf("See in depth\n");
    #endif
}
~~~
```

```
~~~c
(15)main()
{
    int x=3,y=4,z;
    z=x+y;
    #include<string.h>
    printf("%d\n",z);
}
~~~
```

```
~~~c
(16)#define DIFF(FNAME, DTYPE, RTYPE) \
    RTYPE FNAME(DTYPE X, DTYPE Y){ return X-Y;}
DIFF(diff_int,int,int)
DIFF(diff_iptr,int*,int)
DIFF(diff_float,float,float)
DIFF(diff_fptr,float*,int);
main()
{
    int iarr[5]={1,2,3,4,5},a,p,q;
    float farr[7]={1.2,2.3,3.4,4.5,5.6,6.7,7.8},b;
    a=diff_int(iarr[4],iarr[1]);
    b=diff_float(farr[6],farr[2]);
    p=diff_iptr(&iarr[4],&iarr[1]);
    q=diff_fptr(&farr[4],&farr[1]);
    printf("a = %d, b = % .1f, p = %d, q = %d\n",a,b,p,q);
}
~~~
```

```
~~~c
(17)#define MAX 3
main()
{
    printf("Value of MAX is %d\n",MAX);
    #undef MAX
    #ifdef MAX
        printf("Have a good day");
    #endif
}
~~~
```

```
~~~c
(18)#define PRINT1(message) printf(message);
    #define PRINT2(message) printf("message");
~~~
```