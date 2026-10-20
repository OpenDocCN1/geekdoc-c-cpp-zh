```
// Fig. 5.13: ContinueTest.java
// continue statement terminating an iteration of a for statement.
public class ContinueTest
{
    public static void main( String[] args )
    {
        for ( int count = 1; count <= 10; count++ ) // loop 10 times
        {
            if ( count == 5 ) // if count is 5,
                continue; // skip remaining code in loop

            System.out.printf( "%d ", count );
        } // end for

        System.out.println( "\nUsed continue to skip printing 5" );
    } // end main
} // end class ContinueTest
```

1 2 3 4 6 7 8 9 10
Used continue to skip printing 5

# Fig. 5.13 | continue statement terminating an iteration of a for statement.

Figure 5.13 uses continue to skip the statement at line 12 when the nested if (line 9) determines that count’s value is 5. When the continue statement executes, program control continues with the increment of the control variable in the for statement (line 7).

In Section 5.3, we stated that while could be used in most cases in place of for. This is not true when the increment expression in the while follows a continue statement. In this case, the increment does not execute before the program evaluates the repetition-continuation condition, so the while does not execute in the same manner as the for.

# Software Engineering Observation 5.4

Some programmers feel that break and continue violate structured programming. Since the same effects are achievable with structured programming techniques, these programmers do not use break or continue.

# Software Engineering Observation 5.5

There’s a tension between achieving quality software engineering and achieving the best-performing software. Sometimes one of these goals is achieved at the expense of the other. For all but the most performance-intensive situations, apply the following rule of thumb: First, make your code simple and correct; then make it fast and small, but only if necessary.

# 5.8 Logical Operators

The if, if...else, while, do...while and for statements each require a condition to determine how to continue a program’s flow of control. So far, we’ve studied only simple conditions, such as count <= 10, number != sentinelValue and total > 1000. Simple conditions are expressed in terms of the relational operators >, <, >= and <= and the equality operators == and !=, and each expression tests only one condition. To test multiple conditions in the process of making a decision, we performed these tests in separate statements