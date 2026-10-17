# # CHAPTER 13 References

+   * Dereference it using the `&` sign:
+   
+     ```
+     &$addFoods();
+     ```

+   * Use the pointer operator before the parentheses (`->`):
+   
+     ```
+     $addFoods->();
+     ```

Listing13_09 explores the creation of three function references. One prints a list of vegetables when you call it. The other two modify this basic version of the function so that when it appends the names of foods, it adds characters between them. To explore one use of function references, you assign the two forms of the functions into an array and then call the functions using the name of the array and index numbers corresponding to the positions of the function references in the array.

```
```
#Listing13_09
#Function references
#1 Define an array
@Vegetables = ("Green beans", "Broccoli", "Brussels sprouts");
$NL = "\n";

#2 Definition of anonymous functions before their use
$addFoods = sub{
    return join(", ", @_);
};

#3 Definition and assignment to an array
$addMoreFoods[0] = sub{
    return join(" | ", @_);
};

$addMoreFoods[1] = sub{
    return join(" * ", @_);
};

#------------------------------------------------------------
printf(" %25s", "$NL $NL $NL Use of addFoods()");

#4 Using a dereferenced anonymous function
printf("$NL %15s $NL" . &$addFoods(@Vegetables));
```
```