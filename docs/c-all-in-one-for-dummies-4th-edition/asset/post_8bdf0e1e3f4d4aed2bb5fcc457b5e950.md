
```cpp
cout << "Value is: " << arg << endl;
return constraint(arg);
}

template<typename T, typename... Args>
bool ProcessArgs(T arg, Args... args) {
  cout << "Value is: " << arg << endl;
  return constraint(arg) && ProcessArgs(args...);
}

int main()
{
  cout << "List contains only numbers above 7: "
       << (ProcessArgs(10, 11, 14, 8) ? "True" : "False")
       << endl << endl;

  cout << "List contains only numbers above 7: "
       << (ProcessArgs(10, 3, 6) ? "True" : "False")
       << endl;
  return 0;
}
```

The example still outputs each of the values it processes. However, it also checks the constraint and returns true when the number is greater than 7. This extra level of processing is common in certain sciences, especially in statistical analysis, machine learning, or deep learning tasks. An advantage of this approach is that the code doesn’t check every value if one value is out of range. The moment the code detects an incorrect value, it ends the recursion. Here’s the output from this example:

```text
Value is: 10
Value is: 11
Value is: 14
Value is: 8
List contains only numbers above 7: True

Value is: 10
Value is: 3
List contains only numbers above 7: False
```

### Advanced Lambda Expressions

![](img/128ab511de4e7360e167e3b15cdd5dd0_446_0.png)

## Fixing Problems

### Contents at a Glance

- **CHAPTER 1: Dealing with Bugs** ... 429
  - It's Not a Bug, It's a Feature! ... 430
  - Make Your Application Features Look Like Features ... 431
  - Anticipating (Almost) Everything ... 432
  - Avoiding Mistakes, Plain and Simple ... 441
- **CHAPTER 2: Debugging an Application** ... 443
  - Programming with Debuggers ... 444
  - Debugging with Different Tools ... 455
  - Debugging a Code::Blocks Application with Command-Line Arguments ... 456
- **CHAPTER 3: Stopping and Inspecting Your Code** ... 457
  - Setting and Disabling Breakpoints ... 458
  - Watching, Inspecting, and Changing Variables ... 463
- **CHAPTER 4: Traveling About the Stack** ... 469
  - Stacking Your Data ... 470
  - Debugging with Advanced Features ... 475

### IN THIS CHAPTER

- Distinguishing bugs from features
- Anticipating every move the user makes
- Avoiding mistakes the easy way
- Dealing with errors

### Chapter 1: Dealing with Bugs

Who knows whether it's true, but as the story goes, back when the first computer was built over a half-century ago, it filled an entire room with circuitry (yet was about as powerful as one of those inexpensive calculators — the kind that perform only basic math). One day, the thing was misbehaving, and some brave engineers climbed deep into the thing. (The version we're thinking of has them wearing white radiation suits, of course.) Deep in The Bowels of the Machine (sounds like a movie title), they found none other than . . . an insect! A bug! It was a great big bug that had gotten messed up in the circuitry, causing the computer to malfunction. So the story goes, anyway. Today, we use the term *bug* to mean something that is wrong with an application. In this minibook, you discover how to track down bugs and fix them in your software. In this chapter, you see exactly what a bug is (and is not!), how bugs occur, and how you can try to avoid them.

![](img/128ab511de4e7360e167e3b15cdd5dd0_448_0.png)

**REMEMBER**

You don’t have to type the source code for this chapter manually. In fact, using the downloadable source is a lot easier. You can find the source for this chapter in the `\\CPP_A04\\BookIV\\Chapter01` folder of the downloadable source. See the Introduction for details on how to find these source files.

### It’s Not a Bug. It’s a Feature!

So you're using a word processor and suddenly the application freaks out and saves your file automatically. You didn't tell it to do that. Then you use the same copy of the word processor and try to do a copy-and-paste procedure (that's called a use case, by the way). Suddenly the Font dialog box pops up. And then later, you're sitting with your laptop at Starbucks, and it automatically begins the shutdown procedure. You didn't tell it to do that.

Bugs! Bugs! They're all bugs! Or are they? Seems that these pesky little incidents might be considered *features* by some programmers.

Some word processors have an optional *autosave* feature that causes the application to automatically save recovery information in case the computer goes dead. And that Font dialog box that popped up was a user mistake: You meant to press Ctrl-V, but your fingers slipped and caught the D key instead. As it happens, by default Ctrl-D opens the Font dialog box in some word processors. And newer versions of most operating systems understand laptop computers: When the battery is just about to be completely drained, the operating system saves the entire state of the machine to a giant file on the hard drive and shuts down. This is called *hibernation*. So these aren't bugs, after all. Now you can close that bug report you just sent to the vendor.

Now consider this: Suppose that you're using an application and in the middle of it, you get a message box that says something like ExceptionError. Then the application simply closes. All your work is lost. So you call tech support, and the helpful friend on the other end says, “You must have typed something it didn't like. This application has a built-in protection scheme whereby if you type something you're not supposed to, it shuts down.” That's when the guy says, “It's a feature, not a bug!” Unfortunately, sometimes situations walk the fine line between bug and feature. No one would think that an application crashing could be considered a feature, but consider this instead: When your browser messes up, a message asks whether you want it to send the vendor a trouble report. That's a feature that handles bugs.

But the unnamed application that shut down definitely has a bug. And other applications have bugs. For example, you may have been quickly switching between browser windows, typing, resizing, doing things quickly as you go back and forth between the windows, when suddenly the browser crashes and you see the trouble-report message. That really is a bug: The application choked when you, the user, did something that the programmers did not anticipate.

Of course, you wonder why the application choked. In addition to not having planned for some particular input, the programmers might have simply messed up. They didn't include code to handle a rough situation (rapidly switching,

```
C. Compress information.
D. Delete the information.
Your choice:
```

Now suppose that the user chooses D for Delete, and the following menu appears:

```
What would you like to delete?
    A. None of the data; forget it!
    B. Some of the data.
    C. Most of the data.
    D. All the data! Get rid of it all!
```

Now imagine that a user starts this application and sees the first menu. The user doesn’t know whether to type A for the first choice or Add for the first choice. The user types Add and presses Enter. Oops. The A went to the first choice, and the system added the random information and printed the same first menu again. The d (the second character the user typed) then went to the choice Delete the information. That caused the second menu, the Delete menu, to appear. The third character that the user typed, d, caused the second menu’s D selection to take place — All the data! Get rid of it all! — all in one shot, without the user’s realizing what happened.

Oops! What was supposed to be Add turned into Add, Delete, Delete all the data. Not good! How can you avoid this kind of thing?

- Restrict the user's choices.
- Clearly state what the user should do.
- Support multiple options.
- Anticipate what could go wrong.

For example, you might tell the user to type only a single character, with a message such as this:

```
Please enter a single character for your choice:
```

But now, does the user have to press Enter afterward? This message suggests so. But maybe not. So you must be more specific. Maybe one of these examples would work better:

```
Type a single character and do not press Enter:
```

or

```
Type a single character and then press Enter:
```
