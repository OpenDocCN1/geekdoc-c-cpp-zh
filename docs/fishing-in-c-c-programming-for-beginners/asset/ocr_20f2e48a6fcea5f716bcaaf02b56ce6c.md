```
for(i=1;i<7;i++)
{
    for(j=0;j<20;j++)
    {
        cout<<ch[i][j];
        if(i==6)
            exit(0);
    }
    cout<<" \n";
}
return 0;
}
```

# Output

```
CDEF HIJK MNOP RSTU
DEFG IJKL NOPQ STUV
EFGH JKLM OPQR TUVW
FGHI KLMN PQRS UVWX
GHIJ LMNO QRST VWXY
```

Well, this program has used one function exit(0). This is a function used to return to the parent function returning a value which is zero here. This function sometimes requires process.h header file. So, if your compiler shows an error exit() does not have a prototype or exit() undeclared then just include one extra line in your program #include<process.h>

# Passing string to the function

Strings can also be passed to the function. It can be passed in two ways:

+   i. Calling by value
+   ii. Calling by reference