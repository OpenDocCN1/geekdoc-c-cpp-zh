# 6. What is the output of the following program?

```
#include<stdio.h>
int main() {
  char c=124;
  c=c+9; //line 2
  printf("%d",c);
  return 0;
}
```

+   (a) 135
(b) infinite
(c) -8
(d) -123

# 7. What is the output of the following program?

```
#include<stdio.h>
int main() {
  int x, a=5, b=10; //line 1
  x=a+b;
  static int y = x; //line 3
  if(y==x) {
    printf("Hello");
  } else {
    if(y>x) {
      printf("Hi");
    } else {
      printf("Bye");
    }
  }
  return 0;
}
```

+   (a) Hello
(b) Hi
(c) Bye