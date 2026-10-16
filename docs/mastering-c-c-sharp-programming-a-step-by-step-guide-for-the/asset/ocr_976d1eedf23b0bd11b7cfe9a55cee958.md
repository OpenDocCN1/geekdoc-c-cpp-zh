+   - >=
+   - <=

There are some others including +=, -=, *=, /=, ad %=. However, when the + operator is overloaded, it will automatically overload the += operator.

You should also know that when you overload a relational operator, you must do them in pairs. If the == operator is overloaded, so must the != operator be overloaded. And if the > operator is overloaded, you also need to overload the < operator, and so on.

We mustn’t forget that some of the operators have two versions – unary and binary. Take the + operator, for example. The binary version will do operations on two things, for instance, adding 4 + 6 – the operator will apply to both numbers separately. The unary operator, on the other hand, will only do operations on one thing. Take -9 for example; the operator is only applied to the 9, no other number.

What can’t be overloaded?

+   - &&
+   - ||
+   - =
+   - . (dot operator)
+   - new
+   - and a few others that we haven’t looked at.

The [ and ] operator, which is used for indexing, may be overloaded by using indexers, but we will come onto that in the next section.

# Overloading Operators

Operators can be overloaded for any class that you want, but to keep things relatively simple here, I will choose a class that actually makes sense from the overloading perspective. We’ll use the Point class to do the overloading – this stores two coordinates of X and Y. If you understand vectors from physics and math then this will make some sense to you.