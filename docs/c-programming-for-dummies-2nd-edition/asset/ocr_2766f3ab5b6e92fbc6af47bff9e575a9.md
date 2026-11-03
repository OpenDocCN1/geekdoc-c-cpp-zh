# LISTING 8-3: (continued)

```
}
if(guess!=secret)
{
    puts("Wrong!");
    return(1);
}
}
```

Take note of the value returned by the program — either 0 for a correct answer or 1 for a wrong answer. If you're using Code::Blocks or another IDE, you can see this value in the output window.

# Knowing the difference between = and ==

One of the most common mistakes made by every C language programmer — beginner and pro alike — is using a single equal sign instead of a double in an if expression. To wit, I offer Listing 8-4.

# LISTING 8-4: Always True

```
#include <stdio.h>

int main()
{
    int a;

    a = 5;

    if(a=-3)
    {
        printf("%d equals %d\n",a,-3);
    }
    return(0);
}
```

Exercise 8-7: Use the source code shown from Listing 8-4 to create a new program. Ignore any warnings and run the program.