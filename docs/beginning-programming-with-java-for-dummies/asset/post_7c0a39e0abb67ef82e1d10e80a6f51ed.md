
## Chapter 8: Numbers? Who Needs Numbers?

### In This Chapter

- Working with characters
- Dealing with "true" or "false" values
- Rounding out your knowledge of Java's primitive types

I don't particularly like fax machines. They're so inefficient. Send a short fax, and what do you have? You have two slices of a tree — one at the sending end, and another at the receiving end. You also have millions of dots — dots that scan tiny little lines across the printed page. The dots distinguish patches of light from patches of darkness. What a waste!

Compare a fax with an e-mail message. Using e-mail, I can send a 25-word contest entry with just 2,500 zeros and ones, and I don't waste any paper. Best of all, an e-mail message doesn't describe light dots and dark dots. An e-mail message contains codes for each of the letters — a short sequence of zeros and ones for the letter A, a different sequence of zeros and ones for the letter B, and so on. What could be simpler?

Now imagine sending a one-word fax. The word is "true," which is understood to mean, "true, I accept your offer to write *Beginning Programming with Java For Dummies, 4th Edition.*" A fax with this message sends a picture of the four letters t-r-u-e, with fuzzy lines where dirt gets on the paper and little white dots where the cartridge runs short on toner.

But really, what's the essence of the "true" message? There are just two possibilities, aren't there? The message could be "true" or "false," and to represent those possibilities, I need very little fanfare. How about 0 for "false" and 1 for "true"?

They ask, "Do you accept our offer to write *Beginning Programming with Java For Dummies, 4th Edition*?"

"1," I reply.

Too bad I didn't think of that a few months ago. Anyway, this chapter deals with letters, truth, falsehood, and other such things.

### Characters

In Chapters 6 and 7, you store numbers in all your variables. That's fine, but there's more to life than numbers. For example, I wrote this book with a computer, and this book contains thousands and thousands of non-numeric things called characters.

The Java type that's used to store characters is `char`. Listing 8-1 has a simple program that uses the `char` type, and a run of the Listing 8-1 program is shown in Figure 8-1.

**Listing 8-1: Using the char Type**

```java
class LowerToUpper {
    public static void main(String args[]) {
        char smallLetter, bigLetter;

        smallLetter = 'b';
        bigLetter = Character.toUpperCase(smallLetter);
        System.out.println(bigLetter);
    }
}
```

![](img/f938eba5f15e231d828a6255e7ec5523_169_0.png)

In Listing 8-1, the first assignment statement stores the letter `b` in the `smallLetter` variable. In that statement, notice how `b` is surrounded by single quote marks. In a Java program, every `char` literal starts and ends with a single quote mark.

When you surround a letter with quote marks, you tell the computer that the letter isn't a variable name. For example, in Listing 8-1, the incorrect statement `smallLetter = b` would tell the computer to look for a variable named `b`. Because there's no variable named `b`, you'd get a `b cannot be resolved to a variable` message.

In the second assignment statement of Listing 8-1, the program calls an API method whose name is `Character.toUpperCase`. The method `Character.toUpperCase` does what its name suggests — the method produces the uppercase equivalent of a lowercase letter. In Listing 8-1, this uppercase equivalent (the letter `B`) is assigned to the variable `bigLetter`, and the `B` that's in `bigLetter` is printed on the screen, as illustrated in Figure 8-2.

![](img/f938eba5f15e231d828a6255e7ec5523_170_0.png)

**Figure 8-2:** The action in Listing 8-1.

When the computer displays a `char` value on the screen, the computer doesn't surround the character with single quote marks.

### I digress . . .

A while ago, I wondered what would happen if I called the `Character.toUpperCase` method and fed the method a character that isn't lowercase to begin with. I yanked out the Java API documentation, but I found no useful information. The documentation said that `toUpperCase` "converts the character argument to uppercase using case mapping information from the UnicodeData file." Thanks, but that's not useful to me.

Silly as it seems, I asked myself what I'd do if I were the `toUpperCase` method. What would I say if someone handed me a capital `R` and told me to capitalize that letter? I'd say, "Take back your stinking capital R." In the lingo of computing, I'd send that person an error message. So I wondered whether I'd get an error message if I applied `Character.toUpperCase` to the letter `R`.

I tried it. I cooked up the experiment in Listing 8-2.

**Listing 8-2: Investigating the Behavior of toUpperCase**

```java
class MyExperiment {
    public static void main(String args[]) {
        char smallLetter, bigLetter;
        smallLetter = 'R';
        bigLetter = Character.toUpperCase(smallLetter);
        System.out.println(bigLetter);
        smallLetter = '3';
        bigLetter = Character.toUpperCase(smallLetter);
        System.out.println(bigLetter);
    }
}
```

In my experiment, I didn't mix chemicals and blow things up. Here's what I did instead:

-   I assigned `'R'` to `smallLetter`.

    The `toUpperCase` method took the uppercase `R` and gave me back another uppercase `R`. (See Figure 8-3.) I got no error message. This told me what the `toUpperCase` method does with a letter that's already uppercase. The method does nothing.

-   I assigned `'3'` to `smallLetter`.

    The `toUpperCase` method took the digit `3` and gave me back the same digit `3` (see Figure 8-3). I got no error message. This told me what the `toUpperCase` method does with a character that's not a letter. It does nothing, zip, zilch, bupkis.

**Figure 8-3:** Running the code in Listing 8-2.

![](img/f938eba5f15e231d828a6255e7ec5523_171_0.png)

I write about this experiment to make an important point. When you don't understand something about computer programming, it often helps to write a test program. Make up an experiment and see how the computer responds.

I guessed that handing a capital `R` to the `toUpperCase` method would give me an error message, but I was wrong. See? The answers to questions aren't handed down from heaven. The people who created the Java API made decisions. They made some obvious choices, and they also made some unexpected choices. No one knows everything about Java's features, so don't expect to cram all the answers into your head.

The Java documentation is great, but for every question that the documentation answers, it ignores three other questions. So be bold. Don't be afraid to tinker. Write lots of short, experimental programs. You can't break the computer, so play tough with it. Your inquisitive spirit will always pay off.

Reading and understanding Java's API documentation is an art, not a science. For advice on making the most of these docs, read my article "Making Sense of Java's API Documentation," at http://www.dummies.com/extras/beginningprogrammingwithjava.

### One character only, please

A `char` variable stores only one character. So if you're tempted to write the following statements

```java
char smallLetters;
smallLetters = 'barry'; //Don't do this
```

please resist the temptation. You can't store more than one letter at a time in a `char` variable, and you can't put more than one letter between a pair of single quotes. If you're trying to store words or sentences (not just single letters), then you need to use something called a `String`. For a look at Java's `String` type, see Chapter 18.

### Variables and recycling

In Listing 8-2, I use `smallLetter` twice, and I use `bigLetter` twice. That's why they call these things variables. First, the value of `smallLetter` is `R`. Later, I vary the value of `smallLetter` so that the value of `smallLetter` becomes `3`.

When I assign a new value to `smallLetter`, the old value of `smallLetter` gets obliterated. For example, in Figure 8-4, the second `smallLetter` assignment puts `3` into `smallLetter`. When the computer executes this second assignment statement, the old value `R` is gone.
