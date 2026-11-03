Next, clean up the curly brackets, which most veteran programmers prefer to put each on a line by itself.

```
```
1 int main()
2 {
3 }
```
```

Now, let's add a statement to the main function. Note how the editor automatically indents the line. That's the traditional way C code is formatted. Next, type the word “return” and a number. Go ahead and pick any number, although it must be an integer. In our example, we'll type the number 3.

```
```
1 int main()
2 {
3 return(3);
4 }
5
```
```

You can type the number in parenthesis, as what we've done in the example shown above, or you can just specify the value. If so, you need to put a space between return and the value like so:

```
```
1 int main()
2 {
3 return 3;
4 }
5
```
```

Don't forget to type a semi-colon to end the statement. Save the file and then click Build. As long as your code looks like the example shown above, no errors or warnings will appear. Go ahead and click Run.