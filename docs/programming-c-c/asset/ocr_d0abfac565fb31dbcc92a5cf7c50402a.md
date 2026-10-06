```
include<stdio.h>
#include<string.h>
unionData{
    int i;
    float f;
    char str[20];
};
int main(){
    unionData data;
    printf("Memory size occupied by data : %d\n",sizeof(data));
    return 0;
}
```

When the above code is compiled and executed, it produces the following result:
Memory size occupied by data : 20

# Create Union Variables

When a union is defined, it creates a user-defined type. However, no memory is allocated. To allocate memory for a given union type and work with it, we need to create variables.

Here's how we create union variables.

```
union bus
{
    char name[50];
    int price;
};
int main(){
    union bus bus1, bus2, *bus3;
    return 0;
}
```