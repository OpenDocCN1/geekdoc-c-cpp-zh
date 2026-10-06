In the revised code segment, the Appliance class has a Lamp object as a data member. You can easily find the calls to this object, if necessary.

# B.2.4 Avoidance of Global Variables in Modules

One of the many advantages of the concepts of encapsulation and information hiding is the creation of isolated modules. This isolation is sacrificed when a module accesses a global variable, because the effects of a module are no longer self-contained or limited to output arguments. That is, a module has a side effect. Hence, the isolation of errors and limitations is greatly compromised when global variables appear in modules.

Do not use global variables

# B.2.5 Error Handling

A program should check for errors in both its input and its logic and attempt to behave gracefully and consistently when it encounters them. A method should check for certain types of errors, such as invalid argument or null values. What should a method take when it encounters an error? Depending on context, the appropriate action in the face of an error from ignoring the error and continuing to terminate the program. A common technique is for method to return a boolean value to the calling method to indicate that it has encountered an error. Thus, the method leaves error handling to the calling method. In general, methods should either return a value or throw an exception instead of displaying a message when an error occurs.

In case of an error, methods should return a value or throw an exception, but not display a message

# B.2.6 Readability

For a program to be easy to follow, it should have a good structure and design, a good choice of identifiers, good indentation and use of blank lines. These points are demonstrated in the programs throughout this book. You avoid clever programming that saves a little computer time at the expense of much human time

Choose identifiers that describe their purpose—that is, self-documenting. Distinguish between keywords, such as int, and user-defined identifiers. This book uses the following conventions:

+   * Keywords are uppercase and appear in color:
* Names of functions are lowercase.
* User-defined identifiers use both uppercase and lowercase letters, as follows:
    * Class names are nouns, with each word the identifier capitalized.
    * Method names and function names are verbs or action phrases, with the first letter lowercase and subsequent internal words capitalized.
    * Variables begin with a lowercase letter, with subsequent words in the identifier.
    * Data types are declared in a typedef statement and names of enumerations begin with an uppercase letter.
    * Named constants and enumerators are entirely uppercase and use underscores to separate words.

Identifier style

+   * Other naming conventions are suggested as a learning aid:
    * Data types declared in a typedef statement end in Type.
    * Exception names appear in Exception.

Two learning aids

Use a good indentation to enhance the readability of a program. The layout of a program is much easier for a reader to identify the program's modules. Also, within these definitions, you should indent individual blocks of code. These blocks are generally—but are not limited to—the actions performed within a control structure, such as a while loop or an if statement.