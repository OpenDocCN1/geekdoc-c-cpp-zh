# 4. What is the output of the following program?

```
#include<stdio.h>
union unit {
int i;
char str[10]; //line2
} obj;
int main()
{
obj.i = 0;
printf("%s",obj.str);
obj.str = "hello";//line 5
printf("%s",obj.str);
return 0;
}
```

+   (a) hello
(b) hello
(c) error- compile time
(d) error- run time

# 5. Suggest modifications in the above program code that will allow assignment of string "hello" in enum from main() function?

# 6. What is the output of the following program?

```
#include<stdio.h>
union {
int i;
char j;
} obj;
int main()
{
obj.j = 'a';
printf("%d",sizeof(obj));
return 0;
}
```

+   (a) 1