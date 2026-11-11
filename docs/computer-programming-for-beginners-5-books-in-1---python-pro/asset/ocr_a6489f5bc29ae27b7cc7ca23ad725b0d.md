World” example you learned how to print a line of text to your display by using the print functions. Keep in mind that you can use that same function to also print a variable's assigned value, as well as strings of characters. In your program, however, you had one single print statement. Now the question is, how do you print multiple statements in a single line? If you go with the basic method you used in your program, you will find out that you need to print each statement in its own line. Let's introduce you to the concept of string concatenation. Concatenating in this case simply refers to joining strings of text together. You can do this several ways. Here's one example that is done by separating the values with commas:

```
~~~
characterClass = “warrior”

characterGender = “male”

print (characterGender, characterClass)
~~~
```

The output will be “male warrior”.

There are other ways to join bits of text into one line. For instance, you can even eliminate the commas if you are concatenating the strings themselves instead of variables that represent them. Here's how:

```
~~~
print (“male” “warrior”)
~~~
```

The output will be “malewarrior”. Keep in mind that when you use this method, you need to include a space within the string itself if you need it, otherwise the two strings will be combined without one like in this example. Here's how to add the space:

```
~~~
print (“male ” “warrior”)
~~~
```

Now the result will be “male warrior”. However, if you try to concatenate a string with a variable this way, you will have a problem. Here's what happens:

```
~~~
print (characterGender “warrior”)
~~~
```

The result will look something like this:

```
~~~
File "<stdin>", line 1

print (characterGender “warrior”)

^ SyntaxError: invalid syntax
~~~
```