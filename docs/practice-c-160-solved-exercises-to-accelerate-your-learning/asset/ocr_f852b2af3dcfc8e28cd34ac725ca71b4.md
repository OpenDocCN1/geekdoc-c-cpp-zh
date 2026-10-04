```
std::cin >> c;

std::cout << "Enter the height relative to side b: ";std::cin >> h;

// Calculate the perimeter and area
double perimeter = a + b + c;
double area = (b * h) / 2;

// Display the results
std::cout << "The perimeter of the triangle is: " << perimeter << std::endl;
std::cout << "The area of the triangle is: " << area << std::endl;

return 0;
}
```