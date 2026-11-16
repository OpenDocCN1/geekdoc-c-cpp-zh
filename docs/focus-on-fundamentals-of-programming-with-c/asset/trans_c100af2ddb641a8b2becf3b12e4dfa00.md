

看看你能否在下面的程序中找到错误：

```c
// oops.c

#include <stdio.h>
#include <string.h>

int main(void);
char * foo(void);

int main(void) {
    char *buf;

    buf = foo();
    puts(buf);
    return 0;
}

char* foo(void) {
    char buf[32];

    strcpy(buf, "Hello, world.");
    puts(buf);
    return buf;
}
```

问题在于 buf 的存储空间是在栈上分配的，并且是函数 foo() 的局部变量。当 foo() 退出时，栈上的存储空间会被回收，并返回一个不再指向任何有效内存位置的指针。解决这个问题的方法是返回一个指向有效存储位置的指针，该位置在 foo() 退出后仍然持续存在。

```c
// strdup.c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void);
char* foo(void);

int main(void) {
    char *buf;

    buf = foo();
    puts(buf);
    free(buf);
    return 0;
}

char* foo(void) {
    char buf[32];

    strcpy(buf, "Hello, world.");
    puts(buf);
    return strdup(buf);
}
```

strdup() 通过调用 malloc() 在堆上获取存储空间来复制一个字符串。分配的空间长度为 strlen(s) + 1 字节。由于存储空间是在堆上分配的，因此在函数 foo() 退出后它仍然持续存在。请注意，当不再需要时，你有责任通过调用 free() 来释放 strdup() 分配的空间。如果 strdup() 成功，它将返回指向堆上包含复制字符串的位置的指针。否则，如果无法分配空间，它将返回 NULL。

现在让我们来看一个更有趣的动态变量，它是一个用户定义的结构体，而不是一个简单的整数变量。给定以下结构体声明：

```c
typedef struct student {
    char name[30];
    int age;
    float gpa;
} STUDENT;
```

它声明了一个带有三个字段的 student 结构体，并且给定以下指针定义：

```c
STUDENT *ps;
```

它声明指针 ps 是指向 student 结构体的指针，我们可以按照以下方式在堆上动态创建一个 student 结构体变量：

```c
ps = (STUDENT *) malloc(sizeof(struct student));
```

请注意，我们必须将 malloc() 的返回值强制转换为指针 ps 的适当类型，即 STUDENT *，或者指向 student 结构体的指针。我们还必须告诉 malloc() 我们想要为此动态变量在堆上分配的确切字节数，在此例中为 sizeof(struct student) 字节。

现在我们有了一个指向结构体的指针 ps。为了访问结构体的字段，我们必须先解引用指针（以获取结构体本身），然后使用直接成员选择（.）运算符来访问结构体的适当字段。

例如：

```c
*ps.age = 35;
```

不幸的是，这里有一个问题。直接成员选择（.）运算符的优先级高于星号（*）运算符。因此，上述代码会在指针被解引用之前尝试访问结构体的字段。这必然会导致灾难！！简单的解决方法是使用括号来覆盖优先级：

```c
(*ps).age = 35;
```

现在，指向结构体的指针首先被解引用，从而得到结构体本身，然后访问结构体的适当字段。虽然这种语法是正确的，但 C 程序员几乎从不使用它！原因是有一种快捷语法，需要敲击的按键更少，并且产生更清晰的代码。等效语句如下所示：

```c
ps->age = 35;
```

这个间接成员选择运算符 -> 由连字符和大于号组成，中间没有空格。它会自动先解引用指针，然后选择结构体的适当字段。请注意，只有在你拥有指向结构体的指针并且想要访问结构体的字段时，才能使用此运算符。下面的示例展示了这个新运算符的用法：

```c
// student.c

#include <stdio.h>
#include <string.h>
#include <alloc.h>

typedef struct student {
    char name[30];
    int age;
    float gpa;
} STUDENT;

int main(void) {
    STUDENT *ps;

    ps = (STUDENT *) malloc(sizeof(struct student));
    strcpy(ps->name, "Haley Laurel");
    ps->age = 35;
    ps->gpa = 3.75;
    printf("%s is %4.2f\n", ps->name, ps->age, ps->gpa);
    free(ps);
    return 0;
}
```

## 动态数组 - 高级

我们知道可以声明常见数据类型的数组以及用户定义数据类型的数组。例如，我们可以声明一个包含 5 个整数的数组：

```c
int num[5];
```

或者我们可以声明下面程序中所示的包含 5 个 student 结构体的数组：

```c
// array.c

#include <stdio.h>

typedef struct student {
   char name[30];
   int age;
   float gpa;
} STUDENT;

void initialize(STUDENT stud[]); // Function initializes student array.
                                 // Code not included.

int main(void) {
   int i;
   STUDENT stud[5];

   initialize(stud);
   for (i = 0; i < 5; i++) {
      printf("%s %d %4.2f\n", stud[i].name, stud[i].age,
             stud[i].gpa);
   }
}
```

在这个程序中，整个数组的存储空间是在栈上分配的，如下所示：

![](img/7f36c52b5170b89b142dbb7b1ea4666b_444_0.png)

内置或用户定义类型的数组可以存储在堆上并通过指针访问。下面的程序声明了一个指向 `student` 结构体的指针数组。指针数组的存储空间是在栈上分配的，而每个实际 `student` 结构体的存储空间是在堆上分配的。

```c
// darray1.c

#include <stdio.h>
#include <alloc.h>

typedef struct student {
    char name[30];
    int age;
    float gpa;
} STUDENT;

void initialize(STUDENT *pstud[]);
```

```c
void main(void) {
    int i;
    STUDENT *pstud[5];
    for(i = 0; i < 5; i++) {
        pstud[i] = (STUDENT *) malloc(sizeof(struct student));
        initialize(pstud);
    }
    for (i = 0; i < 5; i++) {
        printf("%s %d %4.2f\n", pstud[i]->name, pstud[i]->age,
               pstud[i]->gpa);
    }
    for (i = 0; i < 5; i++) {
        free(pstud[i]);
    }
}
```

下面是前一个程序中创建的动态数组的表示：

![](img/7f36c52b5170b89b142dbb7b1ea4666b_445_0.png)

在堆上动态创建项目数组的另一种方法如下所示：

```c
// darray.c

#include <stdio.h>
#include <stdlib.h>

typedef struct student {
    char name[30];
    int age;
    float gpa;
} STUDENT;

void initialize(STUDENT *pstud);

void main(void) {
    int i;
    STUDENT *pstud;

    pstud = (STUDENT *) malloc(5 * sizeof(struct student));
    initialize(pstud);
    for (i = 0; i < 5; i++) {
        printf("%s %d %4.2f\n", pstud[i].name, pstud[i].age,
               pstud[i].gpa);
    }
    free(pstud);
}
```

如下图所示，在栈上分配的唯一存储空间是指向 student 结构体数组的指针的存储空间。数组本身（即每个 student 结构体）的存储空间是在堆上分配的。

![](img/7f36c52b5170b89b142dbb7b1ea4666b_446_0.png)

在上面的程序中，请注意，我们使用直接成员选择（.）运算符而不是间接成员选择（->）运算符来访问 `struct` 的字段。这是因为这次我们没有指向结构体的指针数组，而是结构体本身包含在数组中。

我们的最后一个示例也在堆上创建了一个动态数组。然而，这次不仅在堆上创建了一个指针数组，而且指针所指向的 `student` 结构体也在堆上创建。

```c
// dynamic3.c

#include <stdio.h>
#include <alloc.h>

typedef struct student {
    char name[30];
    int age;
    float gpa;
} STUDENT;

void initialize(STUDENT **pstud);

void main(void) {
    int i;
    STUDENT **pstud;

    pstud = (STUDENT **) malloc(5 * sizeof(STUDENT *));
    for (i = 0; i < 5; i++) {
        pstud[i] = (STUDENT *) malloc(sizeof(struct student));
        initialize(pstud);
        for (i = 0; i < 5; i++) {
            printf("%s %d %4.2f\n", pstud[i]->name, pstud[i]->age,
                   pstud[i]->gpa);
        }
    }
    for (i = 0; i < 5; i++) {
        free(pstud[i]);
    }
    free(pstud);
}

