Clearly, operators of higher precedence must execute before adjoining operators of lower precedence: in x+y*z, the multiplication must be executed before the addition because the result of the multiplication is the right-hand operand of the addition. However, it is important to realize that precedence and associativity affect only the order in which the *operators* themselves are executed; they do not in any way affect the order in which the *operands* are evaluated.

Operands are always evaluated from left to right in C#. In an expression with three method calls, such as A()*B()*C(), first A() is evaluated, then B(), then C(); then the multiplication operator determines the product; and finally the addition operator determines the sum. Just because C() is involved in a multiplication and A() is involved in a lower-precedence addition does not imply that method invocation C() happens before method invocation A().

# **Language Contrast: C++: Evaluation Order of Operands**

> In contrast to the rule mentioned here, the C++ specification allows an implementation broad latitude to decide the evaluation order of operands. When given an expression such as A()+B()*C(), a C++ compiler can choose to evaluate the function calls in any order, just so long as the product is one of the summands. For example, a legal compiler could evaluate B(), then A(), then C(); then the product; and finally the sum.

# *Using the Addition Operator with Strings*

Operators can also work with non-numeric operands. For example, it is possible to use the addition operator to concatenate two or more strings, as shown in Listing 4.4.

# **LISTING 4.4: Using Binary Operators with Non-numeric Types**

```
class FortyTwo
{
    static void Main()
    {
        short windSpeed = 42;
        System.Console.WriteLine(
            "The original Tacoma Bridge in Washington\nwas "
            + "brought down by a "
            + windSpeed + " mile/hour wind.");
    }
}
```