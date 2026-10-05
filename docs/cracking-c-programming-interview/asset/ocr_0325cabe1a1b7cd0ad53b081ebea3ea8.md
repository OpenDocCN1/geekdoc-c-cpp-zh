```
{
  printf("hello");
}
void ccc() {
  printf("bye");
}
int main() {
  void (*ptr[3])();
  ptr[0]=aaa;
  ptr[1]=bbb;
  ptr[2]=ccc;
  ptr[2]();
  return 0;
}
```

+   (a) hi
(b) hello
(c) bye
(d) error- compile time

# 7. What is the output of the following program?

```
#include<stdio.h>
int main() {
  int a=0; int b=0;char x='\\0'; char y=1;
  if(a,b,x,y) {
    printf("hello");
  } else {
    printf("bye");
  }
  return 0;
}
```

+   (a) hello