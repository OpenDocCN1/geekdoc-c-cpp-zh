```
#include "Time.h"

void main () {
    Time currentTime(9, 14, 30.0);
    currentTime.increment(500.0);
    currentTime.print();

    Time breadTime(3, 35, 0.0);
    Time doneTime.add(breadTime);
    doneTime.print();

    if (doneTime.after(currentTime)) {
        cout << "The bread will be done after it starts." << endl;
    }
}
```

Again, \`main.cpp\` has to include the header file.
It may not be obvious why it is useful to break a small program into three pieces. In fact, most of the advantages come when we are working with larger programs.

Reuse: Once you have written a structure like \`Time\` you might find it useful in more than one program. By separating the definition of \`Time\` from \`main.cpp\` you make it easy to include the \`Time\` structure in another program.

Managing interactions: As systems become large, the number of interactions between components grows and quickly becomes unmanageable. It is often useful to minimize these interactions by separating modules like `Time.cpp\` from the programs that use them.

Separate compilation: Separate files can be compiled separately and then linked into a single program later. The details of how to do this on your programming environment. As the program gets large, separate compilation can save a lot of time, since you usually need to compile only a few at a time.

For small programs like the ones in this book, there is no great advantage to splitting programs. But it is good for you to know about this feature, especially since it explains one of the statements that appeared in the first program we wrote:

```
#include <iostream.h>
.h is the header file that contains declarations for `cin` and `cout` and the functions that operate on them. When you compile your program, you need the information in header file.
```