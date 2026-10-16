```
Console.WriteLine("You got an 'A'");
}
```

```
if(score < 60)
{
// This only gets executed if the score is less than 60.
Console.WriteLine("You got an 'F'. Sorry.");
}
```

You might have spotted that things have turned out a little different to what we originally wanted to do. We wanted an A grade to be assigned if the score was at over 90. Exactly 90 will not result in an A grade because it is not more than 90. That brings us neatly to the final two relational operators - >= and <=. These mean, respectively, greater than or equal to and less than or equal to:

```
if(score >= 90)
{
// This only gets executed if the score is 90 or above...
// Slightly different from the previous example because this one
// also picks up on 90.
Console.WriteLine("You got an 'A'");
}
```

What you have seen here is enough to create the program that we wanted to write in the first place:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```