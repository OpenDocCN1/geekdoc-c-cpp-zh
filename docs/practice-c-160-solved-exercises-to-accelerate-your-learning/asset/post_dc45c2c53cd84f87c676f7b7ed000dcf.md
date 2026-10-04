
# 30. Make a program that reads a value of a product and the tax (in percentage), and calculates the final value of it.

```cpp
#include <iostream>
```

int main() {
    double productValue, taxRate;

    // Prompt the user for the product value
    std::cout << "Enter the value of the product: ";
    std::cin >> productValue;

    // Prompt the user for the tax rate (in percentage)
    std::cout << "Enter the tax rate (in percentage): ";
    std::cin >> taxRate;

    // Calculate the tax amount
    double taxAmount = (taxRate / 100) * productValue;

    // Calculate the final product value including
    double finalValue = productValue + taxAmount;
    // Display the results
    std::cout << "Final value of the product after applying the tax: " << finalValue << std::endl;

    return 0;
}
```

# Conditionals

31. Make a program that asks for a person's age and displays whether they are of legal age or not (age >= 18).

```cpp
#include <iostream>
int main() {
    int age;

    // Prompt the user for their age
    std::cout << "Please enter your age:";
    std::cin >> age;

    // Check if the person is of legal age or not
    if (age >= 18) {
        std::cout << "You are of legal age." << std::endl;
    } else {
        std::cout << "You are not of legal age." << std::endl;
    }
    return 0;
}
```

# 32. Write a program that reads a number and reports whether it is odd or even.

```cpp
#include <iostream>

int main() {
  int number;

  // Prompt the user for a number
  std::cout << "Please enter a number: ";
  std::cin >> number;

  // Determine if the number is odd or even
  if (number % 2 == 0) {
    std::cout << "The number is even." << std::endl;
  } else {
    std::cout << "The number is odd." << std::endl;
  }
  return 0;
}
```

# 33. Write a program that reads a number and reports whether it is positive, negative or zero.

```cpp
#include <iostream>

int main() {
    double number;

    // Prompt the user for a number
    std::cout << "Please enter a number: ";
    std::cin >> number;

    // Determine if the number is positive, negative, or zero
    if(number > 0) {
        std::cout << "The number is positive." << std::endl;
    } else if (number < 0) {
        std::cout << "The number is negative." << std::endl;
    } else {
        std::cout << "The number is zero." << std::endl;
        return 0;
    }
}
```

# 34. Create a program that reads three numbers and checks if their sum is positive, negative or equal to zero

```cpp
#include <iostream>

int main() {
    double num1, num2, num3;

    // Prompt the user for three numbers
    std::cout << "Enter the first number: ";
    std::cin >> num1;

    std::cout << "Enter the second number: ";
    std::cin >> num2;
    std::cout << "Enter the third number: ";
    std::cin >> num3;

    // Calculate the sum of the three numbers
    double sum = num1 + num2 + num3;

    // Determine if the sum is positive, negative, or zero
    if (sum > 0) {
        std::cout << "The sum is positive." << std::endl;
    } else if (sum < 0) {
        std::cout << "The sum is negative." << std::endl;
    } else {
        std::cout << "The sum is zero." << std::endl;
    }

    return 0;
}
```

# 35. Write a program that reads two numbers and tells you which one is bigger.

```cpp
#include <iostream>

int main() {
    double num1, num2;

    // Prompt the user for two numbers
    std::cout << "Enter the first number: ";
    std::cin >> num1;

    std::cout << "Enter the second number: ";
    std::cin >> num2;

    // Determine and display which number is
    if (num1 > num2) {
        std::cout << "The first number (" << num1 << ") is bigger." << std::endl;
    } else if (num1 < num2) {
        std::cout << "The second number (" << num2 << ") is bigger." << std::endl;
    } else {
        std::cout << "Both numbers are equal." << std::endl;
    }

    return 0;
}
```

# 36. Write a program that asks the user for three numbers and displays the largest.

```cpp
#include <iostream>

int main() {
    double num1, num2, num3;

    // Prompt the user for three numbers
    std::cout << "Enter the first number: ";
    std::cin >> num1;

    std::cout << "Enter the second number: ";
    std::cin >> num2;

    std::cout << "Enter the third number: ";
    std::cin >> num3;

    // Determine and display the largest number
    if (num1 >= num2 && num1 >= num3) {
        std::cout << "The largest number is: " << num1 << std::endl;
    } else if (num2 >= num1 && num2 >= num3) {
        std::cout << "The largest number is: " << num2 << std::endl;
    } else {
        std::cout << "The largest number is: " << num3 << std::endl;
    }

    return 0;
}
```

# 37. Make a program that reads three numbers, and informs if their sum is divisible by 5 or not.

```cpp
#include <iostream>

int main() {
    double num1, num2, num3;

    // Prompt the user for three numbers
    std::cout << "Enter the first number: ";
    std::cin >> num1;

    std::cout << "Enter the second number: ";
    std::cin >> num2;

    std::cout << "Enter the third number: ";
    std::cin >> num3;

    // Calculate the sum of the numbers
    double sum = num1 + num2 + num3;

    // Check if the sum is divisible by 5
    if (static_cast<int>(sum) % 5 == 0) {
        std::cout << "The sum of the numbers is divisible by 5." << std::endl;
    } else {
        std::cout << "The sum of the numbers is not divisible by 5." << std::endl;
    }
    return 0;
}
```

# 38. Write a program that asks for an integer and checks if it is divisible by 3 and 5 at the same time.

```cpp
#include <iostream>

int main() {
    int number;
    // Prompt the user for an integer
    std::cout << "Enter an integer: ";
    std::cin >> number;

    // Check if the number is divisible by 3 and 5
    if (number % 3 == 0 && number % 5 == 0) {
        std::cout << "The number is divisible by 3 and 5." << std::endl;
    } else {
        std::cout << "The number is not divisible by 3 and 5." << std::endl;
    }
    return 0;
}
```

# 39. Make a program that asks for two numbers and displays if the first is divisible by the second.

```cpp
#include <iostream>
int main() {
    double num1, num2;

    // Prompt the user for two numbers
    std::cout << "Enter the first number: ";
    std::cin >> num1;

    std::cout << "Enter the second number: ";
    std::cin >> num2;

    // Ensure the second number isn't zero before attempting division
    if (num2 == 0) {
        std::cout << "The second number cannot be zero (division by zero is undefined)." << std::endl;
    } else if (static_cast<int>(num1) % static_cast<int>(num2) == 0) {
        std::cout << "The first number is divisible by the second number." << std::endl;
    } else {
        std::cout << "The first number is not divisible by the second number." << std::endl;
    }

    return 0;
}
```

# 40. Make a program that reads the scores of two tests and reports whether the student passed (score greater than or equal to 6) or failed (score less than 6) in each of the tests.

```cpp
#include <iostream>
int main() {
    double test1Score, test2Score;

    // Prompt the user for scores of two tests
    std::cout << "Enter the score for the first test: ";
    std::cin >> test1Score;

    std::cout << "Enter the score for the second test: ";
    std::cin >> test2Score;

    // Determine and display the result for the first
    if (test1Score >= 6) {
        std::cout << "Passed in the first test." << std::endl;
    } else {
        std::cout << "Failed in the first test." << std::endl;
    }

    // Determine and display the result for the second test
    if (test2Score >= 6) {
        std::cout << "Passed in the second test." << std::endl;
    } else {
        std::cout << "Failed in the second test." << std::endl;
    }

    return 0;
}
```

# 41. Make a program that reads the grades of two tests, calculates the simple arithmetic mean, and informs whether the student passed (average greater than or equal to 6) or failed (average less than 6).

```cpp
#include <iostream>

int main() {
    double test1Grade, test2Grade;

    // Prompt the user for grades of two tests
    std::cout << "Enter the grade for the first test: ";
    std::cin >> test1Grade;

    std::cout << "Enter the grade for the second test: ";
    std::cin >> test2Grade;

    // Calculate the simple arithmetic mean of the
```
