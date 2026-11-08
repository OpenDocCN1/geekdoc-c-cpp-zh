+   ❼ The VARNAME function returns the name of the &i;th variable.
+   ❽ After the information has been retrieved from the metadata, the data set is closed.
+   ❾ This is a macro function and the list of variable names is returned.
+   ❿ The %MAKELIST macro is called with a request for the names of character variables (type=c).

# MORE INFORMATION

DATA step functions that return variable characteristics can be found in Section 3.6.5.

# 13.9 Macro Security and Protection

At times, such as when executing macros under a controlled environment or as part of a larger application, it may be necessary to limit the user’s access to various aspects of the coding of our macros. Sometimes we need to prevent the dissemination of proprietary code. Other times we need to force the use of a particular version of a macro.

When control-related issues are discussed by experienced SAS programmers, common topics include:

+   - What version of a macro is being executed?
+   - How can we control for the correct version?
+   - How do we avoid macro variable collisions and protect our macro variables, compiled macros, and the source code?

# MORE INFORMATION

Sherman and Carpenter (2007) discuss the protection of user IDs and passwords when accessing external databases from within SAS. This topic is also discussed in less detail in Section 5.4.2.

# SEE ALSO

Sun and Carpenter (2011) discuss a number of aspects of the control and protection of macro code, macro operation, and macro variables.

# 13.9.1 Hiding Macro Code

When using stored compiled macros, the SOURCE option on the %MACRO statement can be used to store your macro’s definition, the code itself, in the catalog along with the compiled macro. This code can then be reclaimed from the catalog using the %COPY statement. Of course if your users can see the source code for your macro, they can then re-engineer your macro. Obviously this is definitely not the best way to hide your macro source code.

```
 %macro abc/store source;
```