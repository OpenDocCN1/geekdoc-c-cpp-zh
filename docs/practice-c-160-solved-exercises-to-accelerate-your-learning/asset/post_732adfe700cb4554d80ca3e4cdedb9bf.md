
# 66. Write a program that calculates and displays the value of the power of a number entered by the user raised to an exponent also entered by the user, using repetition loops.

```cpp
#include <iostream>

int main() {
    double base, result = 1.0;
    int exponent;

    // Get input from the user
    std::cout << "Enter the base: ";
    std::cin >> base;

    std::cout << "Enter the exponent (positive or negative integer): ";
    std::cin >> exponent;

    if (exponent > 0) {
        for (int i = 1; i <= exponent; i++) {
            result *= base;
        }
    }
    else if (exponent < 0) {
        for (int i = 1; i <= -exponent; i++) {
            result /= base;
        }
    } // If exponent is 0, result remains 1.0
    std::cout << base << "raised to the power " << exponent << " is:" << result << std::endl;
    return 0;
}
```

# 67. Create a program that displays the first N first perfect squares, where N is informed by the user, using a loop.

```cpp
#include <iostream>
int main() {
    int N;

    // Get input from the user
    std::cout << "Enter the value of N: ";
    std::cin >> N;

    for (int i = 1; i <= N; i++) {
        std::cout << "Square of " << i << " is:" << i*i<< std::endl;
    }

    return 0;
}
```

# 68. Write a program that asks the user for a number N and says whether it is prime or not.

```cpp
#include <iostream>

int main() {
    int N, i;

    // Get input from the user
    std::cout << "Enter a number N:";
    std::cin >> N;

    if (N <= 1) {
        std::cout << N << " is not a prime number." << std::endl;
        return 0;
    }

    for (i = 2; i*i <= N; i++) {
        if (N % i == 0) {
            std::cout << N << " is not a prime number." << std::endl;
            return 0; // If any divisor found, break the loop and print non-prime message
        }
    }

    std::cout << N << " is a prime number." << std::endl;
    return 0;
}
```

# 69. Write a program that prompts the user for a number N and displays all prime numbers less than N.

```cpp
#include <iostream>

int main() {
  int N;

  // Get input from user
  std::cout << "Enter a number N: ";
  std::cin >> N;

  // Print prime numbers less than N
  std::cout << "Prime numbers less than " << N << "are: ";

  for (int num = 2; num < N; num++) {
    bool isPrime = true;

    for (int i = 2; i*i <= num; i++) {
      if (num % i == 0) {
        isPrime = false;
        break; // If any divisor found, set isPrime to false and break the inner loop
      }
    }
    if (isPrime) {
      std::cout << num << " ";
    }
  }

  std::cout << std::endl; // Newline after printing all prime numbers
  return 0;
}
```

# 70. Create a program that displays the first N prime numbers, where N is informed by the user, using a loop.

```cpp
#include <iostream>
int main() {
    int N;

    // Get input from the user
    std::cout << "Enter the number of prime numbers you want: ";
    std::cin >> N;

    std::cout << "The first " << N << " prime numbers are: ";

    int count = 0; // to keep track of the number of primes found
    for (int num = 2; count < N; num++) {
      bool isPrime = true;
      for (int i = 2; i*i <= num; i++) {
        if (num % i == 0) {
          isPrime = false;
          break; // If any divisor found, set isPrime to false and break the inner loop
        }
      }
      if (isPrime) {
        std::cout << num << " ";
        count++;
      }
    }

    std::cout << std::endl; // Newline after printing all prime numbers
    return 0;
}
```

# 71. Write a program that prompts the user for two numbers A and B and displays all numbers between A and B.

```cpp
#include <iostream>

int main() {
    int A, B;

    // Get the two numbers from the user
    std::cout << "Enter the value of A: ";
    std::cin >> A;

    std::cout << "Enter the value of B: ";
    std::cin >> B;
    if (A > B) {
        std::cout << "A should be less than or equal to B.\n";
        return 1; // Exit with error code
    }

    // Display numbers between A and B
    std::cout << "Numbers between " << A << " and " << B << " are:\n";

    for (int i = A; i <= B; i++) {
        std::cout << i << " ";
    }

    std::cout << std::endl; // Newline after printing all numbers
    return 0;
}
```

# 72. Write a program that reads numbers from the user until a negative number is entered, and prints the sum of the positive numbers.

```cpp
#include <iostream>

int main() {
    double number, total = 0;

    std::cout << "Enter numbers (enter a negative number to stop):" << std::endl;

    while (true) {
        std::cin >> number;

        if (number < 0) {
            break; // Exit the loop if a negative number is entered
        }
        total += number;
    }

    std::cout << "Sum of the positive numbers: " << total << std::endl;
    return 0;
}
```

# 73. Write a program that asks the user for a number N and displays the sum of all numbers.

```cpp
#include <iostream>

int main() {
  int N, sum = 0;

  std::cout << "Enter a number N:";
  std::cin >> N;

  for (int i = 1; i <= N; i++) {
    sum += i;
  }

  std::cout << "Sum of numbers up to " << N << " is:" << sum;
  return 0;
}
```

# 74. Write a program that calculates and displays the sum of even numbers.

```cpp
#include <iostream>

int main() {
  int N, sum = 0;

  std::cout << "Enter a number N:";
  std::cin >> N;

  for (int i = 1; i <= N; i++) {
    if (i % 2 == 0) {
      sum += i;
    }
  }

  std::cout << "Sum of even numbers up to " << N << " is:" << sum;
  return 0;
}
```

# 75. Write a program that prompts the user for a number and displays the Fibonacci sequence up to that number.

```cpp
#include <iostream>

int main() {
    int n, t1 = 0, t2 = 1, nextTerm = 0;

    std::cout << "Enter the number of terms: ";
    std::cin >> n;

    std::cout << "Fibonacci Series: ";

    for (int i = 1; i <= n; i++) {
        std::cout << t1 << " ";
        nextTerm = t1 + t2;
        t1 = t2;
        t2 = nextTerm;
    }
    return 0;
}
```

# 76. Write a program that reads numbers from the user until zero is entered, and displays the average of the numbers.

```cpp
#include <iostream>

int main() {
  double sum = 0.0;
  int count = 0;
  double num;

  std::cout << "Enter numbers (enter 0 to stop):" << std::endl;

  do {
    std::cin >> num;
    if (num != 0) {
      sum += num;
      count++;
    }
  } while (num != 0);

  if (count != 0) {
    double average = sum / count;
    std::cout << "Average of the numbers: " << average << std::endl;
  } else {
    std::cout << "No numbers were entered." << std::endl;
  }

  return 0;
}
```

# 77. Write a program that prompts the user for a list of numbers, until the user types the zero, and displays the largest and smallest numbers in the list.

```cpp
#include <iostream>
#include <limits>

int main() {
    double largest = std::numeric_limits<double>::lowest();
    double smallest = std::numeric_limits<double>::max();
    double num;

    std::cout << "Enter numbers (enter 0 to stop): ";

    do {
      std::cin >> num;

      if (num != 0) {
        if (num > largest) {
          largest = num;
        }
        if (num < smallest) {
          smallest = num;
        }
      }
    } while (num != 0);

    if (largest != std::numeric_limits<double>::lowest() && smallest != std::numeric_limits<double>::max()) {
      std::cout << "Largest number: " << largest << std::endl;
      std::cout << "Smallest number: " << smallest << std::endl;
    } else {
      std::cout << "No numbers were entered." << std::endl;
    }

    return 0;
}
```

# 78. Write a program that prompts the user for a number and displays its divisors.

```cpp
#include <iostream>

int main() {
    int num;

    std::cout << "Enter a number: ";
    std::cin >> num;

    std::cout << "Divisors of " << num << " are: ";

    for (int i = 1; i <= num; i++) {
        if (num % i == 0) {
            std::cout << i << "";
        }
    }
}
```
