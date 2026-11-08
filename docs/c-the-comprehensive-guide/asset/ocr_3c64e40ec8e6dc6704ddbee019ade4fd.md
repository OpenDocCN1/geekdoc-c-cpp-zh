+   - You can proactively check the conditions and intermediate results of actions and respond to such behavior in the program: output a message, try again, or terminate the program in an orderly manner.

The latter can usually be done as elaborately as you like. Good handling of unexpected states and errors is a very difficult task.

In C++, you have several options to master this, of which I will discuss two here:

+   - **Error codes**
+     Use return values or output parameters as side information about a process. Check these regularly and handle the event on the spot.

+   - **Exceptions**
+     Instead of passing the error through a side channel, raise an exception at the point of occurrence and *handle* the error elsewhere, probably at a central location for such handling.

First, it must be clear that there are different types of “errors” that need to be handled differently:

+   - **Undesirable state**
+     An undesirable state is an error that you should respond to on the spot because you suspect that something might go wrong. Maybe the document loaded by a user is corrupted. You should be as prepared as possible for such things. In the strictest sense, these are not errors because one definition is that an error is *unexpected* behavior. Error codes play a significant role here. But you can also use exceptions for this.

+   - **Unexpected state**
+     An unexpected state is an error that you do not want to anticipate everywhere—for example, because a check is costly and the consequences of its occurrence do not justify the increased effort of error handling. Memory is running out; the configuration file that was just read has disappeared. For robust software, you need to respond to more of these unexpected states. I wouldn’t say that you *expect* them, but you are simply well prepared. This is where exceptions usually come into play.

+   - **Program error**
+     It is quite possible that your program may enter an undefined state in certain situations. This usually leads to a crash, but not always. You can be aware of this when writing the program and intentionally choose to forgo error handling. You might restrict the input in the documentation, but the documentation is part of the program. There you can write “Do not enter more than 100 numbers”, but nothing prevents users from doing so anyway. Not every program error is a programming error, because it is possible that the program was used incorrectly.

+   - **Programming errors**
+     Programming errors are mistakes that you have unknowingly introduced and that