```
```cpp
int main(int argc, const char *argv[]) {
    /* Input */
    int number {};
    if(argc > 1) {
        number = std::stoi(argv[1]);
    } else {
        std::cout << "Year? "; std::cin >> number;
    }
    /* Calculation */
    Date date = easter(number);  // implicit conversion to Year
    /* Output */
    std::cout << "Easter: " << date << "\n";
}
```
```

# Listing 12.24 Custom data types can protect against errors. This is the first step toward that.

When executed, the program asks for a year like 2024 and then outputs the date of Easter Sunday for that year. You can also call the program from the command line with the year:

```
```text
$ ./33-easter.x 2024
Easter: 2024-03-31
```
```

The function for calculating Easter is a variation of Carl Friedrich Gauss's algorithm. He was the first to devise a simple calculation rule without large tables. In his time, this was one of the most important calculations ever. I will not go into the details of this calculation here.⁴

One line is particularly interesting upon closer inspection:

```
```cpp
Date date = easter(number);
```
```

Here, the int number is automatically converted into a Year for the parameter of easter. Why this happens and how it works is shown in Section 12.11.3, under “Implicit Type Conversion.” There you will also see whether this is a good idea or not.

# 12.11.1  Using Classes as Values

When working with your custom data types, you should treat them no differently than those from the standard library—and actually no differently than the built-in types. When using classes and structs, first consider whether there is any reason not to use them as if they were an int or similar. Only if there is a good reason not to do so should you handle an individual case differently.

⁴ See *Date of Easter*, https://en.wikipedia.org/wiki/Date_of_Easter, [2024-05-19]