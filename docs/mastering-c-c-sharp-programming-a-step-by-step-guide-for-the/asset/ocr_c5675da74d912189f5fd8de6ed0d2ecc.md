```
int wednesday = 4;
int thursday = 5;
int friday = 6;
int saturday = 7;
```

```
int dayOfWeek = tuesday;
```

```
if(dayOfWeek == tuesday)
{
// Do something because this is Tuesday.
}
```

This is exactly what the enumeration is for – creating an enumeration and then listing every value that it could possibly have.

Creating an enumeration must be done outside of any classes that you are using (we’ll talk about classes in another part of the guide). For now, we have just one class in our file, the Program class. The enum keyword is used, you name your enumeration, and then you have all the values it can have in between a set of curly braces:

```
public enum DaysOfWeek { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };
```

Remember, this must be placed outside of the other classes, so your program is going to look like this:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```