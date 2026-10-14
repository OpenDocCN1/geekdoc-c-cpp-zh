# Chapter 22. Operator overloading

After completing this chapter, you will be able to:

+   - Implement binary operators for your own types.
+   - Implement unary operators for your own types.
+   - Write increment and decrement operators for your own types.
+   - Understand the need to implement some operators as pairs.
+   - Implement implicit conversion operators for your own types.
+   - Implement explicit conversion operators for your own types.

The examples throughout this book make great use of the standard operator symbols (such as + and −) to perform standard operations (such as addition and subtraction) on types (such as int and double). Many of the built-in types come with their own predefined behaviors for each operator. You can also define how operators should behave for your own structures and classes, which is the subject of this chapter.

# Understanding operators

It is worth recapping some of the fundamental aspects of operators before delving into the details of how they work and how you can overload them. The following list summarizes these aspects:

+   - You use operators to combine operands into expressions. Each operator has its own semantics, dependent on the type with which it works. For example, the + operator means “add” when you use it with numeric types or “concatenate” when you use it with strings.
+   - Each operator has a precedence. For example, the * operator has a higher precedence than the + operator. This means that the expression a + b * c is the same as a + (b * c).
+   - Each operator also has an associativity that defines whether the operator evaluates from left to right or from right to left. For example, the = operator is right-associative (it evaluates from right to left), so a = b = c is the same as a = (b = c).
+   - A unary operator is an operator that has just one operand. For example, the increment operator (++) is a unary operator.
+   - A binary operator is an operator that has two operands. For example, the multiplication operator (*) is a binary operator.

# Operator constraints

This book presents many examples of how with C# you can overload methods