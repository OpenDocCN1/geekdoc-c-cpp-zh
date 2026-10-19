# Exiting the Loop

These subsections describe handling the end of a loop:

**Assure yourself that the loop ends**  This is fundamental. Mentally simulate the execution of the loop until you are confident that, in all circumstances, it ends. Think through the nominal cases, the endpoints, and each of the exceptional cases.

**Make loop-termination conditions obvious**  If you use a `for` loop and don’t fool around with the loop index and don’t use a `goto` or `break` to get out of the loop, the termination condition will be obvious. Likewise, if you use a `while` or `repeat-until` loop and put all the control in the `while` or `repeat-until` clause, the termination condition will be obvious. The key is putting the control in one place.

**Don’t monkey with the loop index of a for loop to make the loop terminate.**  Some programmers jimmy the value of a `for` loop index to make the loop terminate early. Here’s an example:

![](bbox=[0.087, 0.406, 0.291, 0.508])

```
Java Example of Monkeying with a Loop Index
for ( int i = 0; i < 100; i++ ) {
    // some code
    ...
    if ( ... ) {
        i = 100;
    }
    // more code
    ...
}
```

The intent in this example is to terminate the loop under some condition by setting `i` to 100, a value that’s larger than the end of the `for` loop’s range of 0 through 99. Virtually all good programmers avoid this practice; it’s the sign of an amateur. When you set up a `for` loop, the loop counter is off limits. Use a `while` loop to provide more control over the loop’s exit conditions.

**Avoid code that depends on the loop index’s final value**  It’s bad form to use the value of the loop index after the loop. The terminal value of the loop index varies from language to language and implementation to implementation. The value is different when the loop terminates normally and when it terminates abnormally. Even if you happen to know what the final value is without stopping to think about it, the next person to read the code will probably have to think about it. It’s better form and more self-documenting if you assign the final value to a variable at the appropriate point inside the loop.