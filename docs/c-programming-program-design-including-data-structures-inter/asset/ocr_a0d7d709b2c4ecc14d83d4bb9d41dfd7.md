You can use true and false, instead of 1 and 0, respectively, in the case labels, and rewrite the preceding switch statement as follows:

```
switch (age >= 18)
{
case true:
    cout << "Old enough to be drafted." << endl;
    cout << "Old enough to vote." << endl;
    break;
case false:
    cout << "Not old enough to be drafted." << endl;
    cout << "Not old enough to vote." << endl;
}
```

As you can see from the preceding examples, the switch statement is an elegant way to implement multiple selections. You will see the use of a switch statement in the programming example at the end of this chapter. Even though no fixed rules exist that can be applied to decide whether to use an if...else structure or a switch structure to implement multiple selections, the following considerations should be remembered. If multiple selections involve a range of values, you should use either an if...else structure or a switch structure, wherein you convert each range to a finite set of values.

For instance, in Example 4-23, the value of grade depends on the value of score. If score is between 0 and 59, grade is 'F'. Because score is an int variable, 60 values correspond to the grade of 'F'. If you list all 60 values as case values, the switch statement could be very long. However, dividing by 10 reduces these 60 values to only 6 values: 0, 1, 2, 3, 4, and 5.

If the range of values consists of infinitely many values and you cannot reduce them to a set containing a finite number of values, you must use the if...else structure. For example, if score happens to be a double variable, the number of values between 0 and 60 is infinite. However, you can use the expression static_cast<int>(score) / 10 and still reduce this infinite number of values to just six values.

# Avoiding Bugs by Avoiding Partially Understood Concepts and Techniques (Revisited)

Earlier in this chapter, we discussed how a partial understanding of a concept or technique can lead to errors in a program. In this section, we give another example to illustrate the problem of using partially understood concepts and techniques. In Example 4-23, we illustrate how to assign a grade based on a test score between 0 and 100. Next, consider the following program that assigns a grade based on a test score:

```
//Grade program with bugs.

#include <iostream>                                      //Line 1

using namespace std;                                    //Line 2
```