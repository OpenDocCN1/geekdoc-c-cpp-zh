# Discovering the remainder (modulus)

Of all the basic math operator symbols, % is most likely the strangest. No, it's not the percentage operator. It's the modulus operator. It calculates the remainder of one number divided by another, which is a concept easier to show than to discuss.

Listing 11-3 codes a program that lists the results of modulus 5 and a bunch of other values, ranging from 0 through 29. The value 5 is a constant, mo, which you can easily change later.

# LISTING 11-3: Displaying Modulus Values

```
```c
#include <stdio.h>

int main()
{
    const int value = 5;
    int a;

    printf("Modulus %d:\n",value);
    for(a=0;a<30;a++)
        printf("%d %% %d = %d\n",a,value,a%value);
    return(0);
}
```
```

Line 11 displays the modulus results. The %% placeholder (in Line 10) merely displays the % character, so don't let it throw you.

Exercise 11-7: Type in the source code from Listing 11-3. Save, build, and run.

Now that you can see the output, I can better explain how a modulus operation works. You see its calculation as the remainder of the first value divided by the second. So 20 % 5 is 0, but 21 % 5 is 1.

Exercise 11-8: Change the value constant in Listing 11-3 to 3. Build and run.

# Saving time with assignment operators

If you're a fan of the ++ and -- operators (and I certainly am), you'll enjoy the operators listed in Table 11-2. They're the math assignment operators, and like the increment and decrement operators, they not only do something useful — they also look really cool and confusing in your code.