# Write the routine declaration

Write the routine interface statement—the function declaration in C++, method declaration in Java, function or sub procedure declaration in Microsoft Visual Basic, or whatever your language calls for. Turn the original header comment into a programming-language comment. Leave it in position above the pseudocode you’ve already written. Here are the example routine’s interface statement and header in C++:

Here’s the header comment that’s been turned into a C++-style comment.

Here’s the interface statement.

# C++ Example of a Routine Interface and Header Added to Pseudocode

```
/* This routine outputs an error message based on an error code supplied by the calling routine. The way it outputs the message depends on the current processing state, which it retrieves on its own. It returns a value indicating success or failure. */

Status ReportErrorMessage(
    ErrorCode errorToReport
)
set the default status to "fail"
look up the message based on the error code

if the error code is valid
    if doing interactive processing, display the error message interactively and declare success

    if doing command line processing, log the error message to the command line and declare success

if the error code isn’t valid, notify the user that an internal error has been detected

return status information
```

This is a good time to make notes about any interface assumptions. In this case, the interface variable error is straightforward and typed for its specific purpose, so it doesn’t need to be documented.

# Turn the pseudocode into high-level comments

Keep the ball rolling by writing the first and last statements: { and } in C++. Then turn the pseudocode into comments. Here’s how it would look in the example:

# C++ Example of Writing the First and Last Statements Around Pseudocode

```
/* This routine outputs an error message based on an error code supplied by the calling routine. The way it outputs the message depends on the current processing state, which it retrieves on its own. It returns a value indicating success or failure. */

Status ReportErrorMessage(
    ErrorCode errorToReport
) {
```