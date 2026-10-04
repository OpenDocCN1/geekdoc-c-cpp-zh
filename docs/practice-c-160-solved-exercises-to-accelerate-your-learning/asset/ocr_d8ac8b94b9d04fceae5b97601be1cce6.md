```
std::cout << "Your letter grade is: D" << std::endl;
} else if (grade < 60) {
  std::cout << "Your letter grade is: F" << std::endl;
} else {
  std::cout << "Invalid grade input." << std::endl;
}

  return 0;
}
```

# 52. Write a program that reads the values a, b and c of a quadratic equation, and says if the roots of the function are real or imaginary.

```
#include <iostream>

int main() {
  double a, b, c, discriminant;

  // Read coefficients
  std::cout << "Enter the value of a: ";
```