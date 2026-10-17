In PHP, data input is accomplished using the PHP statement

```
$var_name = trim(fgets(STDIN));
```

where

+   - $var_name can be any variable.
+   - STDIN stands for STANDARD INPUT (this is usually the keyboard).
+   - function trim() is discussed later in this book.

The following code fragment lets the user enter his or her name and age.

```
$name = trim(fgets(STDIN));
$age = trim(fgets(STDIN));
echo "Wow, you are already", age, "years old,", name, "!";
```

It could be even better if, before each data input, a “prompt” message is displayed. This makes the script more user-friendly. For example, look at the following script.

```
echo "What is your name?";
$name = trim(fgets(STDIN));

echo "What is your age?";
$age = trim(fgets(STDIN));

echo "Wow, you are already", age, "years old,", name, "!";
```

The corresponding flowchart fragment looks like this.

![](bbox=[0.15, 0.86, 0.85, 0.97])

Now when a user executes your script he or she knows exactly what to enter.