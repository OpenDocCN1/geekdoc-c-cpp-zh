runtime. However, the results of this probably will not be what you want, as the execution of your code is terminated promptly. The user sees a dialog that complains that your code has not handled the exception and provides any details about the exception the .NET runtime was able to retrieve. At least the exception has been caught!

In general, if you are writing an executable, try to catch as many exceptions as you reasonably can and handle them in a sensible way. If you are writing a library, it is normally best to catch exceptions that you can handle in a useful way, or where you can add additional information to the context and throw other exception types as shown in the previous section. Assume that the calling code handles any errors it encounters.

# User-Defined Exception Classes

In the previous section, you already created a user-defined exception. You are now ready to look at a larger example that illustrates exceptions. This example, called `SolicitColdCall`, contains two nested `try` blocks and illustrates the practice of defining your own custom exception classes and throwing another exception from inside a `try` block.

This example assumes that a sales company wants to increase its customer base. The company’s sales team is going to phone a list of people to invite them to become customers, a practice known in sales jargon as *cold-calling*. To this end, you have a text file available that contains the names of the people to be cold-called. The file should be in a well-defined format in which the first line contains the number of people in the file and each subsequent line contains the name of the next person. In other words, a correctly formatted file of names might look like this:

```
4
George Washington
Benedict Arnold
John Adams
Thomas Jefferson
```

This version of cold-calling is designed to display the name of the person on the screen (perhaps for the salesperson to read). That is why only the names, and not the phone numbers, of the individuals are contained in the file.

For this example, your program asks the user for the name of the file and then simply reads it in and displays the names of people. That sounds like a simple task, but even so a couple of things can go wrong and require you to abandon the entire procedure:

+   - The user might type the name of a file that does not exist. This is caught as a `FileNotFound` exception.
+   - The file might not be in the correct format. There are two possible