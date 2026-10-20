+   - **enumeration list:** This is a list of identifiers, each of which is separated by commas.

In the enumeration list, each symbol represents an integer value. Each symbol will be greater than the one preceding it. The default value of the first symbol in an enumeration list will be 0.

The following example illustrates the use of enumeration variables.

```
using System;

namespace EnumApplication
{

class EnumProgram
{

enum Days { Sun, Mon, tue, Wed, thu, Fri, Sat };

static void Main(string[] args)
{

int WeekdayStart = (int)Days.Mon;

int WeekdayEnd = (int)Days.Fri;

Console.WriteLine("Monday: {0}", WeekdayStart);

Console.WriteLine("Friday: {0}", WeekdayEnd);
```