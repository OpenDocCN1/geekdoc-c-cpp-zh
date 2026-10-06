You write a @return tag for every method that returns a value, even if you have already described the value in the method's description. Try to say something more specific about this value here. This tag may come after any @param tags in the comment. Do not use this tag for void methods and constructors.

Next, if a method can throw an exception, name it by using a @throw tag. You list multiple exceptions alphabetically by name.

Here is a sample comment for a method. We usually begin comments with a brief description of the method's purpose. This javadoc has no tag for it.

```
/** Adds a new entry to a roster.
 * @param newEntry The object to be added to the roster.
 * @param newPosition The position of newEntry within the roster.
 * @pre None.
 * @post If the addition is successful, the roster contains the new entry;
 *       otherwise, the roster is unchanged.
 * @return True if the addition is successful, or false otherwise. */
```

Here is the beginning of a sample class definition that lives in the file someClass.h.

```
/** An example of a class.
 * @file someClass.h
 * @author Ima Student */
```

> **Programming Tip: Comments**
* Use /* ... ... */ comments before the headers of classes and methods to document their use and specifications. Use tags within a comment to identify aspects of the documentation.
* Use // for comments within the body of a class declaration or method definition that describe the details of the implementation.
* Use /* ... ... */ during debugging to temporarily disable a portion of your code.