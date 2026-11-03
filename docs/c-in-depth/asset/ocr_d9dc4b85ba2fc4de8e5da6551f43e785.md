```
{
    err=1;
    break;
}
result=num;
}
if(err==1)
    printf("Overflow\n" );
else
    printf("Result = %u\n",result);
}
```

Now we know very well how to manipulate individual bits within a byte. This bit manipulation is useful in maintaining boolean flags. For example we can use a character variable to hold 8 flags or an integer variable to hold 16 flags. Each bit can be used to represent a flag. This will definitely save memory when many flags are to be used in a program and also it is easy to maintain single variable for several flags. We can test, switch on or off, toggle any individual flag by bitwise operators. Different mask is taken for manipulating each flag. To increase readability, generally each mask corresponding to a flag is given a name using #define. Let us take an example and understand how this is done. We'll declare a variable of unsigned integer type, and then we'll use the individual bits to represent different flags associated with the attributes of a file. The variable is declared as-

```
unsigned int flags;
```

Now we'll use 10 bits of this variable to represent 10 different flags.

![](bbox=[0.15, 0.73, 0.95, 0.88])

To increase readability, we'll give a name to each mask corresponding to these bits.

```
#define _F_RDWR 0x0003    /* Read/write flag        0th and 1st bit */
#define _F_READ 0x0001    /* Read only file         0th bit */
#define _F_WRIT 0x0002    /* Write only file        1st bit */
#define _F_BUF 0x0004     /* Malloc'ed Buffer data  2nd bit */
#define _F_LBUF 0x0008    /* line-buffered file     3rd bit*/
#define _F_ERR 0x0010     /* Error indicator        4th bit*/
#define _F_EOF 0x0020     /* EOF indicator          5th bit*/
#define _F_BIN 0x0040     /* Binary file indicator  6th bit*/
#define _F_IN 0x0080      /* Data is incoming       7th bit*/
#define _F_OUT 0x0100     /* Data is outgoing       8th bit*/
#define _F_TERM 0x0200    /* File is a terminal     9th bit */
```