To export an entity from a module, you simply add `export` in front of its first declaration. In `math.cppm` you see an example of an exported template, an exported variable, an exported enumeration type, and an exported function, `getOddity()`. A second function, `isOdd()`, is purposely not exported. Only module interface files may contain `export declarations`, and only after their module declaration. Only entities that are exported by a module can be used in files that import the module.

Here is how you import the `math` module defined by `math.cppm` and use its exported entities.

```
~~~cpp
// Ex11_01.cpp - Consuming your own module
import <iostream>;
import <format>;
import math;

int main()
{
    std::cout << "Lambda squared: " << square(lambda) << std::endl;

    int number;
    std::cout << "\nPlease enter an odd number: ";
    std::cin >> number;
    std::cout << std::endl;

// if (isOdd(number))      /* Error: identifier not found: 'isOdd' */
//   std::cout << "Well done!" << std::endl;

    switch (getOddity(number))
    {
        using enum Oddity;
        case Odd:
            std::cout << "Well done! And remember: you have to be odd to be number one!";
            break;
        case Even:
            std::cout << std::format("Odd, {} seems to be even?", number);
            break;
    }
    std::cout << std::endl;
}
~~~
```

> > **Note** Before you can compile a file such as `Ex11_01.cpp`, you generally have to compile the interface files of all modules that it imports, which in this case includes that of the `math` module. Compiling a module interface creates a binary representation of all exported entities for the compiler to quickly consult when processing files that import the module. How to compile modules again varies between compilers. Consult the documentation of your compiler for further details.

You import the `math` module by the obvious `import math;` declaration. Unlike with `import` declarations for Standard Library modules, you do not put angle brackets around the name of your own modules. (We refer you to online Appendix A for more information about the use of angle brackets in `import` declarations.)