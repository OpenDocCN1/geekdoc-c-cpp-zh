In published C++ code you sometimes will see a statement such as the following:

```
std::cout << 4 << std::endl;
```

This statement on the surface behaves exactly like the following statement:

```
std::cout << 4 << '\n';
```

but the two expressions `std::endl` and `'
'` do not mean exactly the same thing. The `std::endl` expression does involve a newline character, but it also performs some additional work that normally is not necessary. Programs that do significant printing may execute faster if they terminate their output lines with `'
'` instead of `std::endl`. The difference in speed is negligible when printing to the console, but the different can be great when printing to files or other output streams. For most of the programs we consider, the difference in program execution speed between the two is imperceptible; nonetheless, we will prefer `'
'` for printing newlines because it is a good habit to form (and it requires five fewer keystrokes when editing code).

The three major modern computing platforms are Microsoft Windows, Apple macOS, and Linux. Windows handles newlines differently from macOS and Linux. Historically, the character `'
'` represents a *new line*, usually known as a *line feed* or *LF* for short, and the character `''` means *carriage return*, or *CR* for short. The terminology comes from old-fashioned typewriters which feed a piece of paper into a roller on a carriage that moves to the left as the user types (so the imprinted symbols form left to right). At the end of a line, the user must advance the roller so as to move the paper up by one line (LF) and move the carriage back all the way to its left (CR). Windows uses the character sequence CR LF for newlines, while macOS and Linux use LF. This can be an issue when attempting to edit text files written with an editor on one platform with an editor on a different platform.

The good news is that the C++ standard guarantees that the `std::cout` output stream translates the `'
'` character as it appears in C++ source code into the correct character sequence for the target platform. This means you can print `'
'` via `std::cout`, and it will behave identically on all the major platforms.

In C++ source code, integers may not contain commas. This means we must write the number two thousand, four hundred sixty-eight as 2468, not 2,468. Modern C++ does support single quotes (`'`) as digit separators, as in 2'468. Using digit separators can improve the human comprehension reading large numbers in C++ source code.

In mathematics, integers are unbounded; said another way, the set of mathematical integers is infinite. In C++ the range of integers is limited because all computers have a finite amount of memory. The exact range of integers supported depends on the computer system and particular C++ compiler. C++ on most 32-bit computer systems can represent integers in the range -2,147,483,648 to +2,147,483,647.

What happens if you exceed the range of C++ integers? Try Listing 3.3 (exceed.cpp) on your system.

# Listing 3.3: exceed.cpp

```
#include <iostream>

int main() {
    std::cout << -3000000000 << '\n';
}
```