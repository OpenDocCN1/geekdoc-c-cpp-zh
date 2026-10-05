```
if(*p2 == -1)
break;
if(*p2 >=5 && &p2 <= 10)
{
  (*p1)++;
  if(*p2 > *p3)
    *p3 = *p2;
}
std::cout << *p1 << " students passed (max:" << *p3 << "\n";
return 0;
```

# THE VOID* POINTER

Sometimes we may need to store or pass pointer to a function the memory address of a variable whose we don't know the type. In such cases, the type void is used. The void* pointer is a generic pointer in the sense that it can point to a pointer of any type. A void* pointer can be assigned to another void* pointer. Also, a non-void* pointer can be assigned to another void* pointer. For example:

```
void *p1, *p2;
int i, j, *p3 = &i;
p1 = &j;
p1 = *p3;
p2 = p1;
```

Notice that, except for void*, in order to assign one type to a pointer of another type cast is necessary. For example:

```
char *p1;
int *p2;
...
p2 = p1; // Wrong.
p2 = (int*)p1; // Compiled.n
```

In general, it is better to avoid using castings, as the different sizes of the data types, for example, dereferencing objects, may cause serious problems. If you make a cast, it is better to use a cast operator (e.g., reinterpret_cast) as we will see in Chapter 25.
To access a variable via void* pointer, cast is necessary in order to inform the compiler about the type of variable. For example:

```
#include <iostream> // Example 8.47
int main()
{
  void *ptr;
  char s[] = "abcd";
  int i = 10;

  ptr = &i;
  *ptr += 20; // Wrong, cast is needed.
  *(int*)ptr += 20; // That's ok now.
  std::cout << i << '\n';
```