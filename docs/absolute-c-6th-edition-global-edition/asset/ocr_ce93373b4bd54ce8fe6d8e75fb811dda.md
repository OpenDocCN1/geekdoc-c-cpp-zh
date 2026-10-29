# 8.

```
int index = 0;
while (ourString[index] != '\0' )
{
    ourString[index] = "X";
    index++;
}
```

# 9.

+   a. If the C-string variable does not have a null terminator, '\0', the loop can run beyond the memory allocated for the C-string, destroying the contents of memory there. To protect memory beyond the end of the array, change the while condition as shown in b.

```
while( ourString[index] != '\0' && index < SIZE )
```

# 10.

```
#include <cstring>
//needed to get the declaration of strcpy
...
strcpy(aString, "Hello");
```

# 11.

I did it my way!

# 12.

The string "good, I hope." is too long for aString. A chunk of memory that does not belong to the array aString will be overwritten.

# 13.

The complete dialogue is as follows:

```
Enter some input:
The
time is now.
The-time<END OF OUTPUT
```

# 14.

The complete dialogue is as follows:

```
Enter a line of input:
May the hair on your toes grow long and curly.
May t<END OF OUTPUT
```

# 15.

The complete dialogue is as follows:

```
Enter a line of input:
a b c d e f g
a b END OF OUTPUT
```

# 16.