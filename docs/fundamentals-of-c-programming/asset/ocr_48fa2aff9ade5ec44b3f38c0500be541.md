```
count++;
}
// Print out stars, twice the current row plus one:
// 1. number of stars on left side of tree
// = current row value
// 2. exactly one star in the center of tree
// 3. number of stars on right side of tree
// = current row value
count = 0;
while (count < 2*row + 1) {
    std::cout << "*";
    count++;
}
// Move cursor down to next line
std::cout << "\n";
// Change to the next row
row++;
}
}
/*
 * main
 * Allows users to draw trees of various heights
 */
int main() { // Height of tree
    int height;
    std::cout << "Enter height of tree: ";
    std::cin >> height; // Get height from user
    tree(height);
}
```

Observe that the name height is being used as a local variable in main and as a formal parameter name in tree. There is no conflict here, and the two heights represent two different locations in memory. Furthermore, the fact that the statement

```
tree(height);
```

uses main's height as an actual parameter and height happens to be the name as the formal parameter is simply a coincidence. During the call, the value of main's height variable is copied into the formal parameter in tree also named height. The compiler can keep track of which height is which based on where each is declared.

# 9.4.6 Floating-point Equality

Recall from Listing 4.17 (imprecise5th.cpp) that floating-point numbers are not mathematical real numbers: a floating-point number is finite, and is represented internally as a quantity with a binary mantissa and exponent. Just as 1/3 cannot be represented finitely in the decimal (base 10) number system, 1/10 cannot be represented exactly in the binary (base 2) number system with a fixed number of digits. Often, no problems arise from this imprecision, and in fact many software applications have been written using floating-point numbers that must perform precise calculations, such as directing a spacecraft to a distant planet. In such cases even small errors can result in complete failures. Floating-point numbers can and are used safely and effectively, but not without appropriate care.