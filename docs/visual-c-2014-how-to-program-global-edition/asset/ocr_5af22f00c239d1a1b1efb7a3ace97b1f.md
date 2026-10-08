# Self-Review Exercises

+   j) If there are more method calls that can be stored on the program-execution stack, an
er known as a(n) occurs.
k) The declaration is the portion of an app that can refer to the entity in the
declaration by its unqualified name.
l) It's possible to have several methods with the same name that operate on different
types or numbers of arguments. This feature is called method ___
m) The program-execution stack is also referred to as the stack.
n) A method that calls itself directly or indirectly is a(n) method.
o) A recursive method has two components: one that provides a means for the
recursion to terminate by testing for a(n) case and one that expresses the prob-
blem as a recursive call for a slightly simpler problem than the original call.
p) In an expression-bodied method or read-only property, the symbol __ introduces
the method's or read-only getter's body.
q) Types are __ types or __ types.

+   7.2 For the Class Caps in Fig. 7.8, state the scope of each of the following entities:
a) the variable randomNumber.
b) the variable die1.
c) the method RollDice.
d) the method Main.
e) the variable sumOfDice.

+   7.3 Write an app that tests whether the elements of the Math class methods shown in
Fig. 7.2 actually produced the induced results.

+   7.4 Give the method header for each of the following methods:
a) Method Hypotenuse, which takes two double-precision, floating-point arguments
side1 and side2 and returns a double-precision, floating-point result.
b) Method Smallest, which takes three integers x y and returns an integer.
c) Method Instructions, which do not take any arguments and does not return a value.
[Note: Such methods are commonly used to display instructions to a user.]
d) Method IntDouble, which takes integer argument number and returns a double value.

+   7.5 Find the error(s) in each of the following code segments. Explain how to correct the error.
a) void Go()
{
    Console.WriteLine("Inside method G");
    void H()
    {
        Console.WriteLine("Inside method H");
    }
}
b) int Sum(int x, int y)
{
    int result;
    result = x + y;
}
c) void F(float a)
{
    float a;
    Console.WriteLine(a);
}