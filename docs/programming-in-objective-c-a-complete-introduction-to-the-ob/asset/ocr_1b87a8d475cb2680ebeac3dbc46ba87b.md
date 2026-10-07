# The #import Statement

When you have programmed in Objective-C for a while, you will find yourself developing your own set of macros, which you will want to use in each of your programs. But instead of typing these macros into each new program, the preprocessor enables you to collect all your definitions into a separate file and then include them in your program, using the #import statement. These files--similar to the ones you've previously encountered haven't written yourself--normally with the characters .h and are referred to as header or include files.

Suppose you were to set up some #define statements for the various metric conversions. You might want to define constants that you would need for performing your conversions:

```
#define INCHES_PER_CENTIMETER 0.394
#define CENTIMETERS_PER_INCH (1 / INCHES_PER_CENTIMETER)

#define QUARTS_PER_LITER 1.057
#define LITERS_PER_QUART (1 / QUARTS_PER_LITER)

#define OUNCES_PER_GRAM 0.035
#define GRAMS_PER_OUNCE (1 / OUNCES_PER_GRAM)...
```

Suppose you entered the previous definitions into a separate file system called metric.h. Any program that subsequently needed to use any of the definitions contained in the metric.h file could do so by simply including this preprocessor directive:
#import "metric.h"

This statement must appear before any of the #define statements contained in metric.h. The preprocessor looks for the specified file on the system and effectively copies the contents of the file into the program at the precise point at which the #import statement appears. Any statements inside the file are treated just as if they had been directly pasted into the program at that point.

The double quotes around the header filename instruct the preprocessor to look for the specified file in one or more file directories (typically, first in the directory that contains the source file, but the actual places the preprocessor searches can be in Xcode).

Enclosing the filename within the characters < and > instead, as in
#import <Foundation/Foundation.h>

causes the preprocessor to look for the include file only in the special "system" header directory or directories; the current directory will not be searched. Again, with Xcode, you can specify the directories to be searched.