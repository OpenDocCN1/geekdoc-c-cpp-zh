```
}
int main() {
    std::cout << "string s before call: " << s << std::endl;
    replace('X', 5) = 'Z';
    std::cout << "string s after call: " << s << std::endl;
}
```

# Output of program
string s before call: Hello World
string s in replace(): HelloWorld
string s after call: HelloWorld

The replace function executes it replaces the fifth character of s with an 'X'. The function then returns a reference (implicit pointer) to the fifth character in the string. Next the reference value that is pointed to is changed to 'Z'. The assignment replace('X', 5) = Z to the fifth character of s.

# Independent References

We can declare a variable that is simply a reference variable. This type of variable is called an independent reference. For example:

```
int y = 9;
int& x = y;
```

The independent reference x is another name (alias) for the variable y. An independent reference must be initialized when it is declared because it must point to something when it is declared. A bare declaration such as int& x; will not compile. The following declaration will also not compile:

```
int& x = 5;
```

The reason is that 5 is an ephemeral value that does not have an addressable location (we will discuss this in length later when we look at rvalues). The right hand side