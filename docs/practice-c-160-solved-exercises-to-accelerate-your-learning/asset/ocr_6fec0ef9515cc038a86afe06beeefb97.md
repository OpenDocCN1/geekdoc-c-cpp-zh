```
// Read details for the second person
std::cout << "Enter the name of the second person":";
std::getline(std::cin, name2);
std::cout << "Enter the age of " << name2 << ":";
std::cin >> age2;
std::cin.ignore(); // To clear the newline left by the previous input
```

```
// Read details for the third person
std::cout << "Enter the name of the third person:\
```

```
// Output the details
std::cout << std::endl;
std::cout << name1 << " is " << age1 << " years old." << std::endl;
```