# # Recipe 6: Design Error Handling Policies for Libraries and Applications

# ## Situation

Each part of our application has the ability to handle a unique type of error, such as a database problem, a network outage, or incorrect user input. The only way to handle these issues consistently and thoroughly throughout the program is to have a policy in place. Not only do these policies make debugging and maintenance easier, but they also guarantee that the program will behave predictably even when faced with errors.

# ## Practical Solution

# ## Categorize Errors

**Recoverable Errors:** Errors from which the program can recover, such as temporary network downtimes or invalid user inputs. These typically require user notification and the opportunity to retry the operation.

**Unrecoverable Errors:** Critical issues that prevent the program from continuing, such as a corrupted database or a missing system