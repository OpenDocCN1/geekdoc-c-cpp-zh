```
```text
else {
    // can't do anything because the routine is already error processing
}
else {
    // can't do anything because the routine is already error processing
}

// if the error code isn't valid, notify the user that an
// internal error has been detected
else {
    DisplayInteractiveMessage(
        "Internal Error: Invalid error code in ReportErrorMessage()"
    );
}

// return status information
return errorMessageStatus;
}
```
```

Each comment has given rise to one or more lines of code. Each block of code forms a complete thought based on the comment. The comments have been retained to provide a higher-level explanation of the code. All variables have been declared and defined close to the point they’re first used. Each comment should normally expand to about 2 to 10 lines of code. (Because this example is just for purposes of illustration, the code expansion is on the low side of what you should usually experience in practice.)

Now look again at the spec on page 000 and the initial pseudocode on page 000. The original five-sentence spec expanded to 15 lines of pseudocode (depending on how you count the lines), which in turn expanded into a page-long routine. Even though the spec was detailed, creation of the routine required substantial design work in pseudocode and code. That low-level design is one reason why “coding” is a nontrivial task and why the subject of this book is important.

***Check whether code should be further factored***  In some cases, you’ll see an explosion of code below one of the initial lines of pseudocode. In this case, you should consider taking one of two courses of action:

+   - Factor the code below the comment into a new routine. If you find one line of pseudocode expanding into more code that than you expected, factor the code into its own routine. Write the code to call the routine, including the routine name. If you’ve used the PPP well, the name of the new routine should drop out easily from the pseudocode. Once you’ve completed the routine you were originally creating, you can dive into the new routine and apply the PPP again to that routine.
+   - Apply the PPP recursively. Rather than writing a couple dozen lines of code below one line of pseudocode, take the time to decompose the original line of pseudocode into several more lines of pseudocode. Then continue filling in the code below each of the new lines of pseudocode.

> **Cross-Reference** For more on refactoring, see Chapter 24, “Refactoring.”