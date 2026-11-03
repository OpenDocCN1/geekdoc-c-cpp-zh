to the size of base type of pointer. For example if we have an integer pointer pi which contains address 1000 then on incrementing we get 1002 instead of 1001. This is because the size of int data type is 2. Similarly on decrementing pi, we will get 998 instead of 999. The expression ( pi+3 ) will represent the address 1006. Let us see some pointer arithmetic for int, float and char pointers.

```
int a = 5, *pi = &a;
float b = 2.2, *pf = &b;
char c = 'x', *pc = &c;
```

Suppose the address of variables a, b and c are 1000, 4000, 5000 respectively, so initially values of p1, p2, p3 will be 1000, 4000 and 5000.

+   pi++; or ++pi; pi =1000 + 2 = 1002 (Since int is of 2 bytes)
+   pi = pi-3; pi =1002 - 3*2 = 996
+   pi = pi+5; pi =996 + 5*2 = 1006
+   pi--; or --pi; pi =1006 - 2 = 1004

+   pf++; or ++pf; pf = 4000 + 4 = 4004 (Since float is of 4 bytes)
+   pf = pf-3; pf = 4004 - 3*4 = 3992
+   pf = pf+5; pf = 3992 + 5*4 = 4012
+   pf--; or --pf; pf = 4012 - 4 = 4008

+   pc++; or ++pc; pc = 5000 + 1 = 5001 (Since char is of 1 byte)
+   pc = pc-3; pc = 5001 - 3 = 4998
+   pc = pc+5; pc = 4998 + 5 = 5003
+   pc--; or --pc; pc = 5003 - 1 = 5002

The compiler scales all this arithmetic automatically since it knows the base type of pointer. The arithmetic in the case of char pointer seems to be like ordinary arithmetic because the size of a char is 1 byte. The addresses of variables a, b and c are not affected by these operations, only the pointer moves ahead or backwards.

Suppose pi is an integer pointer that contains address 1000 initially.

![](bbox=[0.25, 0.85, 0.9, 0.95])

(a) pi++;
After incrementing, pointer pi points to address 1002 and if dereferenced(*pi), then it will return the information stored at bytes 1002 and 1003.

![](bbox=[0.25, 0.98, 0.9, 1.0])

(b) pi = pi+2;
Now pi contains address 1006, and if dereferenced it will return information stored at bytes 1006 and 1007.