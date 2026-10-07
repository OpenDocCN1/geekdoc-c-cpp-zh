Introducing Friends 579

One way around this difficulty is to tell everyone (and to remember yourself) that you can only write B * 2.75 but never write 2.75 * B. This is a server-friendly, client-beware solution, and that's not what OOP is about.

However, there is another possibility—using a nonmember function. (Remember, most nonmember operators can be overloaded using either member or nonmember functions.) A nonmember function is not invoked by an object; instead, any values it uses, including objects, are explicit arguments. Thus, the compiler could match the member expression

```
A = 2.75 * B; // might not correspond to a member function
```

to the following nonmember function call:

```
A = operator*(2.75, B);
```

The function would have this prototype:

```
Time operator*(double m, const Time &t);
```

With the nonmember overloaded function, the left operand of an operator expression corresponds to the second argument. Meanwhile, the original member function handles operands in the opposite order—that is, a Time multiplied by a double value. Using a nonmember function solves the problem of getting the operands in the desired order (first double and Time), but it raises a new problem: Nonmember functions cannot directly access private data in a class. Well, at least nonmember functions lack access. But there is a special category of nonmember functions, called *friends*, that can access private members of a class.

# Creating Friends

The first step toward creating a friend function is to declare a prototype in the class declaration and prefix the declaration with the keyword friend:

```
friend Time operator*(double m, const Time &t); // goes in class declaration
```

This prototype has two implications:

+   - Although the operator*() function is declared in the class declaration, it is not a member function. So it isn't invoked by the membership operator.
- Although the operator*() function is not a member function, it has the same access rights as a member function.

The second step is to write the function definition. Because it is not a member function, you don't use the Time:: qualifier. You also don't use the friend keyword in the definition. The definition should look like this:

```
Time operator*(double m, const Time &t) // friend not used in definition
{
    Time result;
    long totalminutes = t.hours * m * 60 + t.minutes * m;
    result.hours = totalminutes / 60;
```