Let's look at a constraint function for our next line of code.  This one is much easier to understand.  It accepts a value, a minimum, and a maximum.  The value will be left alone if it falls within the range or set to either min or max if it is outside of that range depending on which it is closest. Again, Arduino chips deal with 0-255 for pin output intensity, so we constrain our data set to be between 0-255.

```
```
do {

// Some code to execute goes between the curly braces

}
while ( conditional statement);
```
```

The difference here is that this statement doesn't check for its condition until after the ‘do’ block has already run.  These ‘do while’ statements are for when you want a while statement, but you need the code inside to run at least one time.