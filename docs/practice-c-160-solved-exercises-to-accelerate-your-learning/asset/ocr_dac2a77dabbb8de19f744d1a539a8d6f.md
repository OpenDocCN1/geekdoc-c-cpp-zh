```
// Store the original values for later use
temp_a = a;
temp_b = b;
```

```
// Calculate GCD using the Euclidean algorithm
while (b != 0) {
    int remainder = a % b;
    a = b;
    b = remainder;
}
```

```
gcd = a;
```

```
// Calculate LCM
lcm = (temp_a * temp_b) / gcd;
```

```
// Print the result
std::cout << "The LCM of " << temp_a << " and " <<ntemp_b << " is " << lcm << "." << << std::endl;
```

```
return 0;
}
```