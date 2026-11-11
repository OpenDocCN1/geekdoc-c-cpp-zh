```
if(conditional expression)
<Statements to be executed when conditional expression evaluated to true>;
```

When conditional expression returns false value, the control of the program goes to the next statement skipping the current statement, which should be executed when condition expression returns true value. Listing 11 shows an example to use the `if` statement (you can find this example in the `ifStatement.cpp` file on the CD in the `code\chapter2` folder):

# Listing 11: Using the `if` Statement

```
#include<iostream.h>

int main()
{
  int age;
    cout<<"Enter your age"<<endl;
    cin>>age;
  if(age<18)
    cout<<"You are not eligible to vote"<<endl;
  if(age>=18)
    cout<<"You are eligible to vote"<<endl;

  return 0;
}
```

# Output 1: When the value supplied is less than 18

```
Enter your age
17
You are not eligible to vote
```

# Output 2: When the value supplied is greater than or equal to 18

```
Enter your age
24
You are eligible to vote
```

In Listing 11, the value supplied at run-time is set in a variable, named `age`. The statement following the first `if` statement gets executed (Output1) when the conditional expression (`age<18`) evaluates to true. In case the age supplied at run-time is greater than or equal to 18, the statement following the second `if` statement gets executed (Output2).

# Using the if-else Statement

Using the `if-else` statement, a block of code is executed if the condition is true and another block of code is executed if the condition is false. This means that the if clause is