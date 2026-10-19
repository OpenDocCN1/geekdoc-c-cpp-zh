output an error message depending on an error code, and suppose that you call the routine ReportErrorMessage(). Here’s an informal spec for ReportErrorMessage():

ReportErrorMessage() takes an error code as an input argument and outputs an error message corresponding to the code. It’s responsible for handling invalid codes. If the program is operating interactively, ReportErrorMessage() displays the message to the user. If it’s operating in command-line mode, ReportErrorMessage() logs the message to a message file. After outputting the message, ReportErrorMessage() returns a status value, indicating whether it succeeded or failed.

The rest of the chapter uses this routine as a running example. The rest of this section describes how to design the routine.

Cross-Reference For details on checking prerequisites, see Chapter 3, “Measure Twice, Cut Once: Upstream Prerequisites,” and Chapter 4, “Key Construction Decisions.”

# Check the prerequisites

Before doing any work on the routine itself, check to see that the job of the routine is well defined and fits cleanly into the overall design. Check to be sure that the routine is actually called for, at the very least indirectly, by the project’s requirements.

# Define the problem the routine will solve

State the problem the routine will solve in enough detail to allow creation of the routine. If the high-level design is sufficiently detailed, the job might already be done. The high-level design should at least indicate the following:

+   - The information the routine will hide
+   - Inputs to the routine
+   - Outputs from the routine
+   - Preconditions that are guaranteed to be true before the routine is called (input values within certain ranges, streams initialized, files opened or closed, buffers filled or flushed, etc.)
+   - Postconditions that the routine guarantees will be true before it passes control back to the caller (output values within specified ranges, streams initialized, files opened or closed, buffers filled or flushed, etc.)

Cross-Reference For details on preconditions and postconditions, see “Use assertions to document and verify preconditions and postconditions” in Section 8.2.

Here’s how these concerns are addressed in the ReportErrorMessage() example:

+   - The routine hides two facts: the error message text and the current processing method (interactive or command line).
+   - There are no preconditions guaranteed to the routine.
+   - The input to the routine is an error code.
+   - Two kinds of output are called for: the first is the error message, and the second is the status that ReportErrorMessage() returns to the calling routine.
+   - The routine guarantees that the status value will have a value of either Success or Failure.