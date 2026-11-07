```
```cpp
template <class Type>
void linkedStackType<Type>::push(const Type& newElement)
{
    unorderedLinkedList<Type>::insertFirst(newElement);
}

template <class Type>
Type linkedStackType<Type>::top() const
{
    return unorderedLinkedList<Type>::front();
}

template <class Type>
void linkedStackType<Type>::pop()
{
    nodeType<Type> * temp;

    temp = first;
    first = first->link;
    delete temp;
}
```
```

# Application of Stacks: Postfix Expressions Calculator

The usual notation for writing arithmetic expressions (the notation we learned in elementary school) is called **infix notation**, in which the operator is written between the operands. For example, in the expression *a + b*, the operator + is between the operands *a* and *b*. In infix notation, the operands have precedence. That is, we must evaluate expressions from left to right, and multiplication and division have higher precedence than do addition and subtraction. If we want to evaluate the expression in a different order, we must include parentheses. For example, in the expression *a + b × c*, we first evaluate × using the operands *b* and *c*, and then we evaluate + using the operand *a* and the result of *b × c*.

In the early 1920s, the Polish mathematician Jan Lukasiewicz discovered that if operators were written before the operands (**prefix** or **Polish** notation; for example, + *a b*), the parentheses could be omitted. In the late 1950s, the Australian philosopher and early computer scientist Charles L. Hamblin proposed a scheme in which the operators follow the operands (postfix operators), resulting in the **Reverse Polish** notation. This has the advantage that the operators appear in the order required for computation.

For example, the expression:

*a + b * c*

in a postfix expression is:

*a b c* × +

The following example shows various infix expressions and their equivalent postfix expressions.