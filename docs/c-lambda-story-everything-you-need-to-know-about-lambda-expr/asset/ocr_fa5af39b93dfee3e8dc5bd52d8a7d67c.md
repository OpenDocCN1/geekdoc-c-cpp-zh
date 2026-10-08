The above example contains a function BuildAHref which takes two parameters and then builds a <a></a> HTML tag. Based on the input parameters, we build the html variable. If the text is not empty, then we use it as the internal HTML value. Otherwise, we use the link . We want the html variable to be const , yet it's hard to write compact code with the required conditions on the input arguments. Thanks to IIFE we can write a separate lambda with const . Later the variable can be passed to validateHTML.

# # One Note About the Readability

Sometimes having a lambda which is immediately invoked might cause some readability issues.

For example:

```
const auto EnableErrorReporting = [&]() {
    if (HighLevelWarningEnabled())
        return true;

    if (HighLevelWarningEnabled())
        return UsersWantReporting();

};\nif (EnableErrorReporting) {
    // ...
}
```

In the above example, the lambda code is quite complicated, and developers who read the code to decipher not only that the lambda is invoked immediately, but they also have to reason about the EnableErrorReporting type. They might assume that EnableErrorReporting is the closure object and not just a const variable. For such cases, you might consider not using auto so that we can easily see the type. And maybe even add a comment next to the () // call it now.

> More on IIFE: You may want to read the chapter about C++17 changes and see an upgraded version of IIFE.