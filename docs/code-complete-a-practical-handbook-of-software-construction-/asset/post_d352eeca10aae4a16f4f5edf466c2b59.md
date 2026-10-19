
Make sure you have an easy and comfortable understanding of what the routine does and how it does it. If you don’t understand it conceptually, at the pseudocode level, what chance do you have of understanding it at the programming-language level? And if you don’t understand it, who else will?

Cross-Reference For more on iteration, see Section 34.8, "Iterate, Repeatedly, Again and Again."

## Try a few ideas in pseudocode, and keep the best (iterate)

Try as many ideas as you can in pseudocode before you start coding. Once you start coding, you get emotionally involved with your code and it becomes harder to throw away a bad design and start over.

The general idea is to iterate the routine in pseudocode until the pseudocode statements become simple enough that you can fill in code below each statement and leave the original pseudocode as documentation. Some of the pseudocode from your first attempt might be high-level enough that you need to decompose it further. Be sure you do decompose it further. If you’re not sure how to code something, keep working with the pseudocode until you are sure. Keep refining and decomposing the pseudocode until it seems like a waste of time to write it instead of the actual code.

## Code the Routine

Once you’ve designed the routine, construct it. You can perform construction steps in a nearly standard order, but feel free to vary them as you need to. Figure 9-3 shows the steps in constructing a routine.

![](img/649c8eee28c38ca1e062691e45dc9883_261_0.png)

Figure 9-3 You’ll perform all of these steps as you design a routine but not necessarily in any particular order.

### Write the routine declaration

Write the routine interface statement—the function declaration in C++, method declaration in Java, function or sub procedure declaration in Microsoft Visual Basic, or whatever your language calls for. Turn the original header comment into a programming-language comment. Leave it in position above the pseudocode you’ve already written. Here are the example routine’s interface statement and header in C++:

Here’s the header comment that’s been turned into a C++-style comment.

Here’s the interface statement.

**C++ Example of a Routine Interface and Header Added to Pseudocode**

```cpp
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

### Turn the pseudocode into high-level comments

Keep the ball rolling by writing the first and last statements: { and } in C++. Then turn the pseudocode into comments. Here’s how it would look in the example:

**C++ Example of Writing the First and Last Statements Around Pseudocode**

```cpp
/* This routine outputs an error message based on an error code supplied by the calling routine. The way it outputs the message depends on the current processing state, which it retrieves on its own. It returns a value indicating success or failure. */

Status ReportErrorMessage(
    ErrorCode errorToReport
) {
// set the default status to "fail"
// look up the message based on the error code
// if the error code is valid
    // if doing interactive processing, display the error message
    // interactively and declare success

    // if doing command line processing, log the error message to the
    // command line and declare success

// if the error code isn't valid, notify the user that an
// internal error has been detected

// return status information
}
```

The pseudocode statements from here down have been turned into C++ comments.

At this point, the character of the routine is evident. The design work is complete, and you can sense how the routine works even without seeing any code. You should feel that converting the pseudocode to programming-language code will be mechanical, natural, and easy. If you don’t, continue designing in pseudocode until the design feels solid.

Cross-Reference This is a case where the writing metaphor works well—in the small. For criticism of applying the writing metaphor in the large, see “Software Penmanship: Writing Code” in Section 2.3.

### Fill in the code below each comment

Fill in the code below each line of pseudocode comment. The process is a lot like writing a term paper. First you write an outline, and then you write a paragraph for each point in the outline. Each pseudocode comment describes a block or paragraph of code. Like the lengths of literary paragraphs, the lengths of code paragraphs vary according to the thought being expressed, and the quality of the paragraphs depends on the vividness and focus of the thoughts in them.

In this example, the first two pseudocode comments give rise to two lines of code:

**C++ Example of Expressing Pseudocode Comments as Code**

```cpp
/* This routine outputs an error message based on an error code supplied by the calling routine. The way it outputs the message depends on the current processing state, which it retrieves on its own. It returns a value indicating success or failure. */

Status ReportErrorMessage(
    ErrorCode errorToReport
) {
    // set the default status to "fail"
    Status errorMessageStatus = Status_Failure;

    // look up the message based on the error code
    Message errorMessage = LookupErrorMessage( errorToReport );

    // if the error code is valid
        // if doing interactive processing, display the error message
        // interactively and declare success

        // if doing command line processing, log the error message to the
        // command line and declare success

    // if the error code isn't valid, notify the user that an
    // internal error has been detected

    // return status information
}
```

This is a start on the code. The variable *errorMessage* is used, so it needs to be declared. If you were commenting after the fact, two lines of comments for two lines of code would nearly always be overkill. In this approach, however, it’s the semantic content of the comments that’s important, not how many lines of code they comment. The comments are already there, and they explain the intent of the code, so leave them in.

The code below each of the remaining comments needs to be filled in:

**C++ Example of a Complete Routine Created with the Pseudocode Programming Process**

```cpp
/* This routine outputs an error message based on an error code
supplied by the calling routine. The way it outputs the message
depends on the current processing state, which it retrieves
on its own. It returns a value indicating success or failure.
*/

Status ReportErrorMessage(
    ErrorCode errorToReport
) {
    // set the default status to "fail"
    Status errorMessageStatus = Status_Failure;

    // look up the message based on the error code
    Message errorMessage = LookupErrorMessage( errorToReport );

    // if the error code is valid
    if ( errorMessage.ValidCode() ) {
        // determine the processing method
        ProcessingMethod errorProcessingMethod = CurrentProcessingMethod();

        // if doing interactive processing, display the error message
        // interactively and declare success
        if ( errorProcessingMethod == ProcessingMethod_Interactive ) {
            DisplayInteractiveMessage( errorMessage.Text() );
            errorMessageStatus = Status_Success;
        }

        // if doing command line processing, log the error message to the
        // command line and declare success
        else if ( errorProcessingMethod == ProcessingMethod_CommandLine ) {
            CommandLineMessageLog;
            if ( messageLog.Status() == CommandLineStatus_Ok ) {
                messageLog.AddToMessageQueue( errorMessage.Text() );
                messageLog.FlushMessageQueue();
                errorMessageStatus = Status_Success;
            }
        }
```

> The code for each comment has been filled in from here down.

> This code is a good candidate for being further decomposed into a new routine: *DisplayCommandLine-Message()*.
