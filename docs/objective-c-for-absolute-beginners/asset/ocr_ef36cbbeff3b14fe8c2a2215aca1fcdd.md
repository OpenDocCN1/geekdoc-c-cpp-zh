init message, gets executed next: [[HelloWorld alloc] init]. So the init message is sent to the new HelloWorld object created by [HelloWorld alloc]. Now, init simply does base-level initialization of the object. The final return from all this is a pointer to the new object, which is the HelloWorld object.

> NOTE: In Objective-C, whenever objects are sent messages, the code must be within square brackets, [ and ].

Now that we've created a new object, it can be used. Line 25, [myObject printGreeting], puts out our object to use. In this piece of code, we use our newly instantiated object by sending a message, printGreeting. The program will output the text HelloWorld!

Line 27 sends another message to our object, the release message. This message tells the system is finished using the object and to release any system resources associated with It.

Line 28 returns the value 0 to the caller of our main function. This indicates a successful execution.

Line 29 ends the code block and the program.

> NOTE: Messages can also accept multiple arguments. Consider, for example, [myCarObject switchRadioBandTo:FMAndTuneTo:104.7]; The message here would be switchRadioBandTo:TuneTo:. After each colon, the argument values are placed when a message is actually sent. You might also notice these messages are named in such a way as to make interpreting what they actually do easy to understand. Using helpful message names is an ideal convention to follow when developing classes because it makes using the classes much more intuitive. Being consistent in naming messages is also critical.