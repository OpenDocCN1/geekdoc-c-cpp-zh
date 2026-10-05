| Identifier | Description |
| --- | --- |
| put/get_money/time | I/O of special number formats |
| quoted | Quotation marks for input and output |

![](bbox=[0.0, 0.0, 0.0, 0.0])

Table 6.3 The stream manipulators.

# ### 6.2.5 The "endl" Manipulator

Not all manipulators actually change the read or write format. The most important exception is std::endl. It acts like an end-of-line character \n, but has the additional effect of emptying the write buffer—by executing pending write tasks. This takes time; after all, buffering was invented specifically to speed things up. If possible, it is better to use \n for a line feed.

You should only use std::endl if you want to be sure that a screen output is received by your users at a specific time.

If you only want to output the retained buffer and no additional line feed, use the flush manipulator—for example, cout << flush.

Before a file is closed—that is, before the program ends or the stream variable becomes invalid—you do not need an additional flush or endl. Closing the file automatically empties the buffer. Only if your program crashes could unwritten remnants remain in the buffer.