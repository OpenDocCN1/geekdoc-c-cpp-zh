+   3. The scope of an identifier declared within a block runs from its declaration to the __________.
+   
+   4. The scope of a parameter is the __________.
+   
+   5. What will the following statements produce?
+   
+   ```cpp
+   for (int i = 0; i < 3; i++)
+       cout << i << endl;
+   cout << "i is now " << i << endl;
+   ```

# Section 10.5

+   1. __________ is the phenomenon of a function referencing itself.
+   
+   2. Name and describe the two parts of a recursive definition of a function.
+   
+   3. (True or false) A nonrecursive function for computing some value may execute more rapidly than a recursive function that computes the same value.
+   
+   4. For the following recursive function, find f(5).

```
```cpp
int f(int n)
{
    if (n == 0)
        return 0;
    else
        return n + f(n - 1);
}
```
```

+   5. For the function in Question 4, find f(0).
+   
+   6. For the function in Question 4, suppose + is changed to * in the inductive step. Find f(5).
+   
+   7. For the function in Question 4, what happens with the function call f(-1)?

# Section 10.6

+   1. A function’s __________ is a list of the types of its parameters.
+   
+   2. Two functions are said to be overloaded if they have the same __________.
+   
+   3. A function’s name can be overloaded provided no two definitions of the function have the same __________.
+   
+   4. A __________ is a pattern from which a function can be constructed.
+   
+   5. Templates may have __________ parameters, but ordinary functions may not.
+   
+   6. Given the template definition

```
```cpp
template<typename something>
void print(something x)
{
    cout << "***" << x << "***\n";
}
```
```