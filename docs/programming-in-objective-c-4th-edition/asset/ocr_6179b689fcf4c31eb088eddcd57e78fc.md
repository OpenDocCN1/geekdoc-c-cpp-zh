assignment statement.

Because the to and from pointers are incremented each time after the assignment statement inside the for loop is executed, they should be incorporated into the assignment statement as post-increment operations. The revised for loop of Program 13.16 then becomes this:

```
for ( *from != '\ 0'; )
    *to++ = *from;
```

Execution of the assignment statement inside the loop would proceed as follows. The character from points to would be retrieved, and then from would be incremented to point to the next character in the source string. The referred character would be stored inside the location that to points to; then would be incremented to point to the next location in the destination string.

The previous for statement hardly seems worthwhile because it has no initial expression and no looping expression. In fact, the logic would be better served when expressed in the form of a while loop. This has been done in Program 13.17, which presents the new version of the copyString function. The while loop uses the fact that the null character is equal to the value 0, as experienced Objective-C programmers do.

# Program 13.17

```
// Function to copy one string to another
// pointer version 2

#import <Foundation/Foundation.h>
void copyString(char *to, char *from)
{
    while (*from )
```