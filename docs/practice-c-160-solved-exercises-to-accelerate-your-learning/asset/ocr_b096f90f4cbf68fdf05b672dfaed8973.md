```
int main() {
    double num1, num2, num3;

    // Prompt the user for three numbers
    std::cout << "Enter the first number: ";
    std::cin >> num1;

    std::cout << "Enter the second number: ";
    std::cin >> num2;

    std::cout << "Enter the third number: ";
    std::cin >> num3;

    // Calculate the arithmetic mean
    double mean = (num1 + num2 + num3) / 3;

    // Display the result
    std::cout << "The arithmetic mean of " << num1
    << "," << num2 << " and " << num3 << " is:" <<
    mean << std::endl;

    return 0;
}
```