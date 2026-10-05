
braces. This grouping of statements has a special meaning in several respects. On the one hand, they can be repeated together in the for loop, and on the other hand, this grouping forms a scope of validity for the variables it contains.

- if(value % divider == 0)... is an if statement, a branching statement. A condition is tested and the following statement `std::cout << ""; is only executed if this condition is true. As with the for loop in the example, we could have followed this with a statement block in {...}(that would have been good style). For demonstration purposes, the if is only followed by a single statement. This way I could save the surrounding {...} for a statement block.
- The return statement `return 0;` concludes this enumeration.

Statements are made up of expressions. An expression can have a value as a result at runtime. At compile time, the compiler knows the type of each expression. We will go into expressions in great detail later. Here are just a few examples from the program:

- value % divider calculates the modulo—that is, the remainder of a division.
- ... == checks the equality of two values.
- divisor+1 is the result of an addition.
- divisor = ..., an assignment, is also an expression.

## 4.2 A Detailed Walkthrough

Having looked at an example program from start to finish in the previous section, I will now go into a little more detail. You will see the first formal definitions and learn to recognize the important language elements.

Let's build Listing 4.1 a little and let's take a closer look at the elements we already know.

```
// https://godbolt.org/z/ceT6Oszxd
#include <iostream> // for std::cin, std::cout, std::endl
#include <string> // std::stoi

void calculate(int n) {
    using namespace std;
    std::endl;
    /* output divisors */
    cout << "divisors of " << n << " are:\n";
    if(n == 0) { cout << "\n"; return; } // 0 is divisor of 0
    for(int divider=1; divider <= n; ++divider) { // for
        divider
        if(n % divider == 0) {
            cout << divider << ",";
        }
    }
    cout << endl;
}

 main(int argc, const char* argv[]) {
    /* Determine number * */
    int value = 0;
    if(argc==1) {
        std::cout << "Enter a number: "; // read into variable
        std::cin >> value; // check whether
        if(std::cin) {
            return 1; // error on user input
        } else {
            value = std::stoi(argv[1]);
        }
    }
    calculate(value);
 // function call
return 0;
}
```

**Listing 4.2** This program asks its users for a number.

To begin with, you will see some new features: I have now introduced a separate calculate function. It receives a parameter of type int, which I address within the function under the name n.

Suddenly main() also has parameters—namely, int argc and const char* argv[]. This allows users to call the program on the command line with the number for which the calculation is to be performed. Here, argc contains the number of arguments that you can query argv[...]. As argv[0] always contains the name of the called program, the first parameter is in argv[1], and so on.

If the program is called without arguments, something must be entered at std::cin >> value.

std::stoi(argv[1]); converts a data type for the first time—in this case, a textual value (const char*) into a number (int). Then I use calculate(value) to call my own function calculate with the variable value.

In addition

### 4.2.1 Spaces, Identifiers, and Tokens to the compiler

which are (as good as) meaningless for the compiler, there is also the space character, the tabulator, and the line break, which the compiler greatly simplifies when reading the source code: all these whitespaces are “collapsed” and only considered as a single separator. It therefore does not matter whether you write return 0; or return 0 ;;, insert line breaks, or even insert blank lines.

A small note on line breaks: this generic term covers the different variants that exist on the different systems. If you see a line break in the editor, different byte sequences end up in the text file on Windows and Linux, and on an old Mac it was another different one. While Linux stores the value 13 (CR, for carriage return), Windows stores the two values 13 and 10 (additional LF, for line feed). Most editors today can cope with both. But this difference is why you always have to specify whether you want to open a binary file or a text file when opening files programmatically.

Ultimately, it is only important that the compiler gets the smallest units cleanly separated from each other—tokens. If these are names (of variables, functions, etc.), then the boundary is clear—namely, where the name ends: the first character that is not suitable for a name is then the boundary. Names (or more precisely identifiers) contain letters and digits as well as a digit. But at the beginning, there must not be a digit. hello, Howdy, GoodDay, w3lc0me, and moin_main are all possible identifiers. In addition to whitespace, a word can also be delimited by special characters such as braces or punctuation. Most of these characters are each a token, and you can insert any amount of space between them without changing the meaning of the program. However, there are a few characters that only retain their meaning if they are written together—and thus count as a token.

When it comes to truth values, you will encounter && || as well as == and !=. In addition, -> and :: are also important for navigating data structures. All other (special) characters are each a token. These include, for example: + - * / % . ( ) [ { } < > ;

Exceptions are: you write a fixed value directly into the source code. This can be an integer such as 100, a floating-point number such as 99.95, or a text such as "Donald E. Knuth"—and for all of these there are also variants in the notation. I will go into more detail. Literals can sometimes look as if they consist of several tokens but as a single one.

```
// https://godbolt.org/z/33cc3xf6
#include <iostream> // must be at the beginning of the line
int main() {
    std::cout << "This is "
"text with <brackets>\n"; // string literal interrupted by line
    /*type:*/ int
    /*Variable:*/ a
    /*Init:*/ 100; // inner comments no spaces
    std::cout<<";";
}
```

**List 4.3** A very unusually formatted piece of source code.

It becomes tricky when a construct is composed of several identifiers. For example, in std::sin() there is the scope resolution operator ::. With templates, you will encounter pairs of angle brackets <...>—for example, in numeric_limits<int>::max() or map<int,string>. All elements are individual valid identifiers, but together do they form a unit.

### 4.2.2 Comments

You have already seen comments with //. If there is not enough space to the end of the line, you can also have a comment extend over several lines by starting it with /* and ending it with */. For example, like you see in the next example.

```
int main() {
    /* My first program. It was written by Max Muster.*/
}
```
