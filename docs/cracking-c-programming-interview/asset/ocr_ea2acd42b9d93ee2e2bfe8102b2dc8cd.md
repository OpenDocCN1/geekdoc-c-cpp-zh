```
return 0;
}
```

+   (a) error- compile time
(b) line 5:: Undefined Behavior, line 7:: Undefined Behavior
(c) line 5:: 1, line 7:: Undefined Behavior
(d) Segmentation Fault

# 39. What is the output of the following program?

```
#include<stdio.h>
struct student {
    int roll ;
    char name[0];
};
struct student *sl = malloc(sizeof(int)); //line 1
int main() {
    sl->roll = 1;
    printf("%d %s",sl->roll,sl->name); //line 4
    return 0;
}
```

+   (a) garbage
(b) 1 <nothing get printed>
(c) error at line 4
(d) error at line 1

# 40. What is the output of the following program?

```
#include<stdio.h>
struct student {
    int roll ;
    char name[0];
}
int main() {
    struct student *sl = malloc(sizeof(int)+10); // line 1
```