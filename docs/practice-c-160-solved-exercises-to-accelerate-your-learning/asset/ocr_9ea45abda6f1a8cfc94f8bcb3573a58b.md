```
int main() {
    double radius;

    // Prompt the user for the radius of the sphere
    std::cout << "Enter the radius of the sphere: ";
    std::cin >> radius;

    // Calculate the volume of the sphere
    double volume = (4.0 / 3.0) * PI * pow(radius, 3);

    // Display the result
    std::cout << "The volume of the sphere with radius " << radius << " is: " << volume << " cubic units" << std::endl;

    return 0;
}
```