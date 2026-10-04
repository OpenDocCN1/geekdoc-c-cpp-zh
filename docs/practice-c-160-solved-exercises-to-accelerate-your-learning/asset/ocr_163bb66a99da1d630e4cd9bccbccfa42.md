```
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