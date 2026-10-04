```
std::cin >> price;

// Determine tax rate based on price
if (price > 500) {
    tax = 0.075; // 7.5%
} else if (price > 200) {
    tax = 0.05; // 5%
} else {
    tax = 0; // No tax
}

// Calculate final price
finalPrice = price + (price * tax);

// Print the final price
std::cout << std::fixed << std::setprecision(2);
std::cout << "The final price of the product (including tax) is: " << finalPrice << std::endl;

return 0;
```