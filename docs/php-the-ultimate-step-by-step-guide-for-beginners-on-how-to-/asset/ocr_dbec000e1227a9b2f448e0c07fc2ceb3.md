unintentionally adjust a variable without acknowledging what the results are. This\sort of error can be extremely hard to find. Also, when we examine functions in detail, you will discover that you can send values to functions when you call them and get values returned from them when they're done. You don't need to use global variables.

On the off chance that you need to use a variable in a particular function without losing the worth every time the function ends, however you would prefer not to use a global variable, but rather use a static variable.

+   - Static variables

Static variables give a variable that isn't decimated when a function ends. You can utilize the static value again whenever you call the capacity and it will have the same value as when it was last utilized as a part of the function. The easiest approach to consider this is to think about the variable as global open to simply that. The estimation of $age is currently held every time the birthday function is called. The worth will stay around until the program ends. Value is prized on the grounds that it's announced as static. In this way, we've talked about two types of variables, yet there's still one more to examine, super globals.

+   - Super global variables

Super global variables, PHP uses uncommon variables called super globals to give data about the PHP script's surroundings. These variables don't require any announcement as global. They are habitually accessible, and they give imperative data past the script's code itself, for example, values from a user's input.

Since PHP 4.01, the super globals are termed as arrays. Arrays are unique accumulations of values that we'll talk about in later chapters. The more established global variables such as those beginning with $HTTP_* that were not in clusters still exist, but rather their use is definitely not recommended, as they are deprecated.