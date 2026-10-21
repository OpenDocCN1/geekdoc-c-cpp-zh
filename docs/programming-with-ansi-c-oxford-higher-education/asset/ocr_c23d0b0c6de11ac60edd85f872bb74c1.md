instead of

```
bool CheckPass(int TotalMarks, int PassingMarks)
```

and there will be no prototype then.

It is possible to have more than one default argument with more than one normal argument. The rule to pass those arguments is very simple. All the normal arguments must be passed before the default arguments in the argument list.

The CheckPass() function prototype can be rewritten as follows (assuming the code is changed to accommodate usage of other parameters):

```
CheckPass(int Sub1Marks, int Sub2Marks, int PassingMarks = 50)
```

```
CheckPass(int Sub1Marks, int Sub2Marks, int PassingMarks1 = 50,
int PassingMarks2 = 35);
```

```
CheckPass(int Sub1Marks, int PassingMarks1 = 50, int Sub2Marks,
int PassingMarks2 = 35);
```

```
/* This statement is wrong because PassingMarks1 is a default argument written before Sub2Marks, which is not a default argument. */
```

# 4.5.1 Using Static Variable as Default Argument to a Function

Functions with default arguments are very handy if, for most of the cases, the value of the argument remains the same. An interesting thing to note here is that a static variable can also be used as a default argument value. So it is possible to write

```
Account(AccountNumber = NextNumber)
```

where NextNumber is a static variable and is incremented every time a new Account object is created. This is an example which shows how an important functionality can be added to a program. As soon as a new account is created, it will get a unique account number automatically. This can be illustrated with a simple example shown in the following program. The getNext() function automatically receives the next immediate number. It can be observed that the static integer value Next is incremented and returned from the function.

This simple solution is possible only in cases where the next number series starts from zero and will not work if the getNext() series is supposed to start from some other number. Such a program will need some changes.

```
#include <iostream>
using namespace std;
static int Next;
int getNext(int NextNumber = Next)
{
    Next++;
    return NextNumber;
}
int main()
{
```