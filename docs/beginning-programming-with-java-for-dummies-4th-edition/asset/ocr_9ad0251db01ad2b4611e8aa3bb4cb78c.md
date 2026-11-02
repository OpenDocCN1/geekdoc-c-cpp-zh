So when you run the code in Listing 19-3, the flow of action in each loop iteration isn't exactly from the top to the bottom. Instead, the action goes from the for loop to the display method and then back to the for loop. The whole business is pictured in Figure 19-4.

Figure 19-4:
The flow of control between Listings 19-1 and 19-3.

![](bbox=[0.22, 0.26, 0.88, 0.65])

# Using punctuation

In Listing 19-3, notice the use of dots. To refer to the lastName stored in the anAccount object, you write

```
anAccount.lastName
```

To get the anAccount object to display itself, you write

```
anAccount.display();
```

That's great! When you refer to an object's variable or call an object's method, the only difference is parentheses:

+   - To refer to an object's variable, you don't use parentheses.
+   - To call an object's method, you use parentheses.

![](bbox=[0.12, 0.9, 0.2, 1.0])

When you call a method, you put parentheses after the method's name. You do this even if you have nothing to put inside the parentheses.