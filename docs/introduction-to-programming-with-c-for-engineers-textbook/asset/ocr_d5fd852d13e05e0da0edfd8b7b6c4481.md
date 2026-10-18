# 3.13.2.4　The goto Statement

The goto statement can be used to immediately change execution to any place in a single function, marked with a label (identifier). This statement stems from the lower-level assembly language paradigm in which jump and compare statements were sufficient for all types of control, including loop organization, as outlined in the hardware model in Section 2.1. Although it might seem useful in some situations, its use is strongly discouraged due to a number of problems. The most frequent are memory leaks due to the omitted memory de-initialization operator, as well as obfuscated code that is hard to understand and maintain. Hence, goto should never be used in new code, although it may be seen in some older libraries (especially those written in C). The other language constructions are sufficient to organize any type of loop(s).

|  | Flowchart | Description | Syntax | Examples |
|---|---|---|---|---|
| goto statement | [flowchart illustration] | Causes an immediate and unconditional change of execution – a jump to a label. Should be avoided in code. | `goto label;` | ```cpp
const int kBufLen = 1024;
char buf[ kBufLen ];

// Read line-by-line
for( ifstream inFile("File.txt"); inFile && ! inFile.eof(); )
{
    if( ! inFile.getline( buf, kBufLen ) )
        goto exit; // exit the loop

    // process buffer ...
}

exit:
    cout << "Loop terminated" << endl;
```

This example of a goto statement causes an immediate and unconditional jump to the place marked with the exit label. Thus, in a single leap, goto can jump through nested loops and functions. Although such code is sometimes used, it is not recommended due to possible memory leaks if objects were allocated in abandoned blocks of code. Also, using goto makes code hard to analyze and maintain. |

# 3.13.2.5　Structural Exception Handling – The try-catch Statement

The try-catch statement, combined with the throw operator (see GROUP 15, Table 3.15), is a C++-only construction that allows exception handling. This means any code that encounters a serious error that cannot be handled in a conventional way can throw an object that represents an exception. This, in turn, can be caught if a throwing function is embedded in a try-catch construct. There are many types of serious errors, such as division by 0, dereferencing a nullptr pointer, insufficient memory, inaccessible resources, etc., as well as situations specific to a given library.