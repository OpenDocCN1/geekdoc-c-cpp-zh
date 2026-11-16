# Listing 4.19: bitwiseoperators.cpp

```
#include <iostream>

int main() {
    int x, y;
    std::cout << "Please enter two integers: ";
    std::cin >> x >> y;
    std::cout << x << " & " << y << " = " << (x & y) << '\n';
    std::cout << x << " | " << y << " = " << (x | y) << '\n';
    std::cout << x << " ^ " << y << " = " << (x ^ y) << '\n';
    std::cout << "~" << x << " = " << ~x << '\n';
    std::cout << x << " << " << 2 << " = " << (x << 2) << '\n';
    std::cout << x << " >> " << 2 << " = " << (x >> 2) << '\n';
}
```

Developers use bitwise operations for a variety of systems-level programming tasks. For example, in a graphical user interface (GUI), the user generates events by interacting with an application using the mouse and a keyboard. One might be clicking a mouse button over a particular graphical element (like a button) within a window. Multiple pieces of information about this event can be stored in a single integer. For example, bit 0 may indicate whether or not the Shift key was held down when the mouse button was clicked. Bit 1 may be responsible for the Alt key, bit 2 for the Ctrl key, etc. Thus the integer value 5, which in binary is

00000000000000000000000000000101

means that when the mouse button was clicked both the Shift and Alt keys were being held down. This might require a different action on the part of the program than if some other combination of keys (or none) were being pressed. For example, suppose the int variable key_status holds information about which keys the user was depressed during the most recent mouse click. Consider the expression key_status & 1. The bit string

00000000000000000000000000000001

represents the expression 1, and the value of key_status is unknown, so key_status & 1 is

```
key_status = ?????????????????????????????????
&       1₁₀ = 00000000000000000000000000000001₂
0₁₀ or 1₁₀ = 00000000000000000000000000000000₂ or 00000000000000000000000000000001₂
```

If the answer is zero, this means bit 0 is 0 in key_status, and so the Shift key is not depressed. On the other hand, if the answer is one, this means bit 0 is 1, and so the Shift key is depressed. In the expression

```
key_status & 1
```

the 1 is called a mask, since it serves to mask off, or “remove” the first 31 bits of key_status.

Usually the GUI library will define constants that help programmers examine or modify particular bits; for example, given the following constants:

```
const int SHIFT_DOWN = 1;       // This is 0...0001
const int CTRL_DOWN = SHIFT_DOWN << 1; // This is 0...0010
const int ALT_DOWN = CTRL_DOWN << 1;   // This is 0...0100
```