# The Dot Operator

The dot operator is used to specify a member variable of a structure variable.

# SYNTAX

StructureVariableName.MemberVariableName

```
struct StudentRecord
{
    int studentNumber;
    char grade;
};
int main()
{
    StudentRecord yourRecord;
    yourRecord.studentNumber = 2001;
    yourRecord.grade = 'A';
```

Some writers call the dot operator the structure member access operator although we will not use that term.

# Structures as Function Arguments

A function can have call-by-value parameters of a structure type and/or call-by-reference parameters of a structure type. The program in Display 10.1, for example, includes a function named getData that has a call-by-reference parameter with the structure type CDAccount.

A structure type can also be the type for the value returned by a function. For example, the following defines a function that takes three appropriate arguments and returns a value of type CDAccount:

```
CDAccount shrinkWrap(double theBalance, double theRate, int theTerm)
{
    CDAccount temp;
    temp.balance = theBalance;
    temp.interestRate = theRate;
    temp.term = theTerm;
    return temp;
}
```

Notice the local variable temp of type CDAccount; temp is used to build up a complete structure value, which is then returned by the function. Once you