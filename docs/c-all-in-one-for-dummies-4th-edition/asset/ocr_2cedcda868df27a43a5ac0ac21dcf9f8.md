respectively. In an assignment statement, an lvalue is any expression that can be on the left side of the equals sign, and an rvalue is an expression that can be on the right side of an equals sign.

![](bbox=[0.17, 0.163, 0.252, 0.235])

The terms lvalue and rvalue don't refer to what happens to be on the left side and right side of an assignment statement. They refer to what is allowed or not allowed on the left or right side of an assignment statement. You can have only lvalues on the left side of an assignment statement and rvalues on the right side of an assignment statement. Here are some examples, in which ploggle is an int type. This is allowed because ploggle is an lvalue:

```
```
ploggle = 3;
```
```

On the left side, you cannot have items that are strictly an rvalue. The following is not allowed because 2 is strictly an rvalue:

```
```
2 = ploggle;
```
```

The number 2 can't appear on the left (setting it equal to something else makes no sense), therefore it isn't an lvalue. In fact, anything you can set equal to something else is an lvalue.

The main reason you need to know these terms is their tendency to show up in error messages. If you try to compile the line 2 = ploggle, you see an error message similar to this one:

```
```
non-lvalue in assignment
```
```

If you don't know what the term lvalue means, these messages can be confusing. Although seeing the problem with 2 = ploggle is pretty easy, sometimes the problem is not that obvious. Look at this:

```
```
ChangeMe() = 10;
```
```

In most cases, putting a function call on the left doesn't make sense, so you don't do it. In other words, you must consider whether the expression ChangeMe() is considered an lvalue. Look at this code from the LValueAndRValue example:

```
```
#include <iostream>

using namespace std;

int uggle;
```
```