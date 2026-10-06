```
break;
case 100:
printf("number is equal to 100");
break;
default:
printf("number is not equal to 10, 50 or 100");
}
return 0;
}
```

Output:
Enter a number:4number is not equal to 10, 50 or 100\enter a number:50number is equal to 50

# Switch case example 2:

```
#include <stdio.h>
int main() {
    int x = 10, y = 5;
    switch(x>y && x+y>0) {
        case 1:
            printf("hi");
            break;
        case 0:
            printf("bye");
            break;
        default:
            printf(" Hello bye ");
    }
}
```

Output:
hi