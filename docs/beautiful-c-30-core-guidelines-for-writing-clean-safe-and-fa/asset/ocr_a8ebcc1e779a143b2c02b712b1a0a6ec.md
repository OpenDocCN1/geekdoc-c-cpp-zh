```
```cpp
int amend_content(std::string const& format,
std::string& destination);
```
```

The return value is an int, the input is the format parameter, while the output is the destination parameter. The caller must create their own string before calling the function, passing this string as the second parameter.

This gives rise to a potential pitfall. How do you know where the input param-eters end and the output parameters begin? Additional documentation is required of the author to ensure that the user arranges their arguments correctly. The function declaration should look something like this:

Click here to view code image

```
```cpp
int amend_content(std::string const& format,
                /*output parameter*/
std::string& destination);
```
```

In this example, you might think that a non-const reference is hinting clearly to the user that this is going to be written to. However, you should assume nothing about your users, and this documentation is a maintenance burden just waiting to be over-looked. The addition of further input and output parameters, for example addi-tional format details or an error channel, demands that the documentation be kept up to date.

There is also the matter of deciding which of the output values should be the return value rather than an output parameter. Some might want the function to return the revised string rather than the amount of data added to it. This can lead to utterly tiresome and vacuous arguing for no real benefit as use cases are presented to the programming team and decisions boil down to who is the squeakiest wheel.

A single return value, on the other hand, is self-documenting: it is, by definition, an output value.

# Documenting and annotating