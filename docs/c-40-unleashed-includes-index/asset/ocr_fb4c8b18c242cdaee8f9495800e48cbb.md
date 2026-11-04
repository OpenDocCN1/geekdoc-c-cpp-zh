# Exceptions Are Objects

One question is how errors are represented in the world of exceptions. Given that the CLR is an object-oriented platform, the answer is pretty obvious: objects. We won't look at how to define exception types of our own just yet but will instead focus on the essence of such a type and look at how exceptions can be thrown and caught.

Exceptions are subtypes of a class called System.Exception, which defines the following useful members (see Figure 8.1). (I've omitted a few irrelevant details for now.)

![](bbox=[0.08, 0.37, 0.56, 0.66])

FIGURE 8.1 Most relevant members of the Exception base type.

One key piece of information about an exception lies outside its members: the type name of the exception itself. For example, an error signaling a missing file will be represented as a FileNotFoundException, deriving from the System.Exception type in one way or another. Compare this to the meaningless integral value 2 used in the Win32 API to represent such a condition. (To verify this for yourself, you can print the corresponding message at the command line by running net helpmsg 2.)

A second piece of information is found in the Message property, which contains a string explaining the problem. This can be shown to the user but is useful during debugging, too. One string message can be worth a thousand cryptic error codes. HelpLink is sometimes populated with a URI to available help information.

Other more-technical error details can be retrieved through the StackTrace property, which dumps information about the location where the error happened in terms of the call stack. This highlights a key aspect of the exception mechanism in the CLR: Errors propagate automatically through the call stack as long as they're not caught. Contrast this with the manual and error-prone propagation of error codes.