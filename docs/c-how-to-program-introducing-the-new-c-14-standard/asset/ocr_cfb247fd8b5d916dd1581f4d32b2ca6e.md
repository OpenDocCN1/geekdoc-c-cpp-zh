+   the `myAccount` object, `getName` “knows” which object’s data to manipulate.
+   
+   2. Next, member function `getName` performs its task—that is, it *returns* (i.e., gives back) `myAccount`’s name to line 13 where the function was called. The main function does not know the details of how `getName` performs its task.
+   
+   3. The `cout` object displays the name returned by member function `getName`, then the program continues executing at line 16 in `main`.

In this case, line 13 does not display a name, because we have not yet stored a name in the `myAccount` object.