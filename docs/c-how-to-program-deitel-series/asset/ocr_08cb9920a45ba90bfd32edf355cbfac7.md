use the class template’s template parameter T to represent the element type. Our Stack class template does not define its own constructors—the default constructor provided by the compiler will invoke the deque’s default constructor. We also provide the following member functions in Fig. 18.1:

+   - `top` (lines 12–15) returns a reference to the Stack’s top element.
+   - `push` (lines 18–21) places a new element on the top of the Stack.
+   - `pop` (lines 24–27) removes the Stack’s top element.
+   - `isEmpty` (lines 30–33) returns a bool value—true if the Stack is empty and false otherwise.
+   - `size` (lines 36–39) returns the number if elements in the Stack.

Each of these member functions delegates its responsibility to the appropriate member function of class template deque.

# Declaring a Class Template’s Member Functions Outside the Class Template Definition

Though we did not do so in our Stack class template, member-function definitions can appear outside a class template definition. If you do this, each must begin with the template keyword followed by the same set of template parameters as the class template. In addition, the member functions must be qualified with the class name and scope resolution operator. For example, you can define the pop function outside the class-template definition as follows:

```
template< typename T >
inline void Stack<T>::pop()
{
    stack.pop_front();
} // end function template pop
```

Stack<T>:: indicates that pop is in the scope of class Stack<T>. The Standard Library’s container classes tend to define all their member functions inside their class definitions.

# Testing Class Template Stack<T>

Now, let’s consider the driver (Fig. 18.2) that exercises the Stack class template. The driver begins by instantiating object doubleStack (line 9). This object is declared as a Stack<double> (pronounced “Stack of double”). The compiler associates type double with type parameter T in the class template to produce the source code for a Stack class with elements of type double that actually stores the elements in a deque<double>.

Lines 16–21 invoke push (line 18) to place the double values 1.1, 2.2, 3.3, 4.4 and 5.5 onto doubleStack. Next, lines 26–30 invoke top and pop in a while loop to remove the five values from the stack. Notice in the output of Fig. 18.2, that the values do pop off in last-in, first-out order. When doubleStack is empty, the pop loop terminates.

```
1  // Fig. 18.2: fig18_02.cpp
2  // Stack class template test program.
3  #include <iostream>
4  #include "Stack.h" // Stack class template definition
```

Fig. 18.2  |  Stack class template test program. (Part 1 of 3.)