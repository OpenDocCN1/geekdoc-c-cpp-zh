```
```c
b=&a;
c=&b;
printf("Address of a =%d\n",&a);
printf("Address of a =%d\n",&b);
printf("Address of a =%d\n",&*c);
printf("Address of b =%d\n",&b);
printf("Address of b=%d\n",&*c);
printf("Address of c=%d\n",&c);
printf("Value of b=%d\n",b);
printf("Value of c=%d\n",c);
printf("Value of a=%d\n",a);
printf("Value of a=%d\n",*(&a));
printf("Value of a=%d\n",*b);
printf("Value of a=%d\n",**c);
}
```
```

The output of the above program would be: Address

Address of a=9876
Address of a =9876
Address of b =8765
Address of b =8765
Address of c =7654
Value of b=9876
Value of c=8765
Value of a =5
Value of a =5
Value of a =5
Value of a =5

Would help you in tracing out how the program prints the above output.

a b c 5 9876 8765 9876 8765 7654.