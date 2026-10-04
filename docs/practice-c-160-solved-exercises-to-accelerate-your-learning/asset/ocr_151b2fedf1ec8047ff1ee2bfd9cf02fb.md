```
int main() {
    double x;
    double cosine_of_x = 1.0;

    // Get input from user
    std::cout << "Enter the value of x (in radians): ";
    std::cin >> x;

    double power_of_x = 1.0; // Initialize with 1 for the first term
    double factorial = 1.0; // Initialize with 1 for the first term
    double term = 1.0; // value of the first term
    int n = 0; // start with n = 0

    // Calculate cos(x) using the Taylor series until the difference between terms is less than 0.001
    while (fabs(term) >= 0.001) {
        n++; // increase n by 1
        power_of_x = x * x; // Calculate x^(2n)
        factorial *= (2*n - 1) * (2*n); // Calculate (2n)!
        term = power_of_x / factorial; // Calculate the
```