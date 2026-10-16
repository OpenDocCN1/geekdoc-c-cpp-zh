declare the exception in its own **throws** clause and not handle it, which effectively propagates the exception to an enclosing **try** clause, if there is one, or to the method's caller, if there is no enclosing **try** clause.
There are no default exception handlers, and it is not possible to disable exceptions. Continuation in Java is exactly as in C++.

# 14.3.5  An Example

Following is the Java program with the capabilities of the C++ program in Section 14.2.5:

```
```java
// Grade Distribution
// Input: A list of integer values that represent
//        grades, followed by a negative number
// Output: A distribution of grades, as a percentage for
//         each of the categories 0-9, 10-19, ..., 
//         90-100.
//
import java.io.*;
// The exception definition to deal with the end of data
class NegativeInputException extends Exception {
    public NegativeInputException() {
        System.out.println("End of input data reached");
    } /** end of constructor
} //** end of NegativeInputException class

class GradeDist {
    int newGrade,
        index,
        limit_1,
        limit_2;
    int [] freq = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0};

    void buildDist() throws IOException {
        DataInputStream in = new DataInputStream(System.in);
        try {
            while (true) {
                System.out.println("Please input a grade");
                newGrade = Integer.parseInt(in.readLine());
                if (newGrade < 0)
                    throw new NegativeInputException();
                index = newGrade / 10;
                try {
                    freq[index]++;
                } /** end of inner try clause
                catch (ArrayIndexOutOfBoundsException e) {
                    if (newGrade == 100)
                        freq[9]++;
                    else
                        System.out.println("Error -- new grade: " +
                                           newGrade + " is out of range");
```
```