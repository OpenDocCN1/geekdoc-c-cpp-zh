```
// Base case: If b is 0, then a is the GCD
if (b == 0) return a;

// Recursive case: Find GCD of b and the remainder
when a a is divided by b
return gcd(b, a % b);
}

int main() {
    int num1, num2;
    std::cout << "Enter first number: ";
    std::cin >> num1;
    std::cout << "Enter second number: ";
    std::cin >> num2;

    int result = gcd(num1, num2);
    std::cout << "GCD of " << num1 << " and " << num2 << " is:" << result << std::endl;

    return 0;
}
```