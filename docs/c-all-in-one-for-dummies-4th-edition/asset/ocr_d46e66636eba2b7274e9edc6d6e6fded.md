```
Compiled at 15:19:38

*** total ***
79800
```

Note, at the beginning, that the code tests for the symbol UNIVAC. But that if block is a bit more complex because it also has an #elif (else if) construct. The language of the preprocessor has no elseif or anything like it. Instead, you have to write it like so:

```
#elif defined(HAL2000)
```

With this block, the preprocessor checks for the symbol UNIVAC; if the preprocessor finds UNIVAC, it spits out these lines:

```
const int total = 200;
const string comname = "UNIVAC";
```

Otherwise, the preprocessor looks for HAL2000; if the preprocessor finds it, it adds these lines to the fixed-up code:

```
const int total = 300;
const string comname = "HAL2000";
```

And finally, if neither UNIVAC nor HAL2000 is set, the preprocessor adds these lines:

```
const int total = 400;
const string comname = "My Computer";
```

Remember that in each case, these two lines are sent out to the fixed-up version in place of the entire block starting with #ifdef UNIVAC and ending with #endif. If you add UNIVAC to the #defines tab of the Project Build Options dialog box shown previously in Figure 2–2, you change how the preprocessor configures its output. To see the following output, you must choose Build➜Rebuild, and then Build➜Run, rather than use the Build➜Build and Run command as normal.

```
Welcome to UNIVAC
Total is:
200

*** max ***
10
```