```
```cpp
// calling the recursive constexpr function recursiveFactorial
std::cout << "\n\nCALCULATING FACTORIALS AT COMPILE TIME "
          << "WITH A RECURSIVE CONSTEXPR FUNCTION"
          << "\nrecursiveFactorial(0): " << recursiveFactorial(0)
          << "\nrecursiveFactorial(1): " << recursiveFactorial(1)
          << "\nrecursiveFactorial(2): " << recursiveFactorial(2)
          << "\nrecursiveFactorial(3): " << recursiveFactorial(3)
          << "\nrecursiveFactorial(4): " << recursiveFactorial(4)
          << "\nrecursiveFactorial(5): " << recursiveFactorial(5);

// calling the iterative constexpr function iterativeFactorial
std::cout << "\n\nCALCULATING FACTORIALS AT COMPILE TIME "
          << "WITH AN ITERATIVE CONSTEXPR FUNCTION"
          << "\niterativeFactorial(0): " << iterativeFactorial(0)
          << "\niterativeFactorial(1): " << iterativeFactorial(1)
          << "\niterativeFactorial(2): " << iterativeFactorial(2)
          << "\niterativeFactorial(3): " << iterativeFactorial(3)
          << "\niterativeFactorial(4): " << iterativeFactorial(4)
          << "\niterativeFactorial(5): " << iterativeFactorial(5) << "\n";
}
```
```

```
```text
CALCULATING FACTORIALS AT COMPILE TIME WITH A RECURSIVE METAFUNCTION
Factorial(0): 1
Factorial(1): 1
Factorial(2): 2
Factorial(3): 6
Factorial(4): 24
Factorial(5): 120

CALCULATING FACTORIALS AT COMPILE TIME WITH A RECURSIVE CONSTEXPR FUNCTION
recursiveFactorial(0): 1
recursiveFactorial(1): 1
recursiveFactorial(2): 2
recursiveFactorial(3): 6
recursiveFactorial(4): 24
recursiveFactorial(5): 120

CALCULATING FACTORIALS AT COMPILE TIME WITH AN ITERATIVE CONSTEXPR FUNCTION
iterativeFactorial(0): 1
iterativeFactorial(1): 1
iterativeFactorial(2): 2
iterativeFactorial(3): 6
iterativeFactorial(4): 24
iterativeFactorial(5): 120
```
```

**Fig. 15.19** | Calculating factorials at compile-time. (Part 2 of 2.)

# Metafunctions

You can perform compile-time calculations with metafunctions. Like the functions you’ve defined so far, metafunctions have arguments and return values, but their syntax is significantly different. Metafunctions are implemented as class templates—typically using structs. A metafunction’s arguments are the items used to specialize the class template, and its return value is a public class member. The type traits introduced in Section 15.5 are metafunctions.