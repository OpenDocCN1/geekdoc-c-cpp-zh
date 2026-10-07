# Chapter 5 Loops and Relational Expressions

```
cout << "Your first name, please: ";
cin >> name;
out << "Here is your name, verticalized and ASCIIized:\n";
int i = 0; // start at beginning of string
while (name[i] != '\0') // process to end of string
{
    cout << name[i] << " : " << int(name[i]) << endl;
    i++; // don't forget this step
}
return 0;
```

Here is a sample run of the program in Listing 5.13:
Your first name, please: Muffy
Here is your name, verticalized and ASCIIized:

+   M: 77
u: 117
f: 102
f: 102
y: 121

> (No, verticalized and ASCIized are not real words or even good would-be words. they do not add the endearing technoid tone to the output.)

# Program Notes

The while condition in Listing 5.13 looks like this:
while (name[i] != '\0')

It tests whether a character in the array is the null character. For this test to eventually succeed, the loop body needs to change the value of i. It does so by incrementing i. Omitting this keeps the loop stuck on the same array, printing the character and the code until you manage to kill the program. Getting an infinite loop is one of the most common problems with loops. Often can cause it when you forget to update some value within the loop body.
You can rewrite the while line like this:

```
while (name[i])
```

With this, the program works as it did before. That's because when name[i] is an ordinary character, its value is the character code, which is nonzero, or true. But name[i] is the null character, its character-code value is 0, or false. This notation is more concise (and more commonly used) than Listing 5.13 uses. Dumb compilers might produce faster code for the second version, but smart compilers produce the same code for both.