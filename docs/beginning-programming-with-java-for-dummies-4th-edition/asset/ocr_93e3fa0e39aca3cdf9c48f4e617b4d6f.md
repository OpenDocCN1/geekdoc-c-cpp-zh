# Escapism

In Figure 12-5, you see the numbers 8, 8, then 6 14 (and so on) displayed. I wanted these numbers to be right under the heading words Card and Total, so I used a trick to make the numbers line up correctly. Normally, I can get perfect vertical columns by pressing the tab key, but a computer program creates the nicely-aligned output in Figure 12-5. How did I get a computer program to press the tab key?

In Java, there’s a way. You can insert a tab in your output by putting `\t` inside double quote marks.

```
System.out.println
        ("Card\tTotal");

System.out.print(card);
System.out.print("\t");
```

```
System.out.println(total);
```

In the first statement, the computer displays Card, then jumps to the next tab stop on the screen, and displays Total. In the next three statements, the computer displays a card number (like the number 6), then jumps to the next tab stop (directly under the word Total), and displays a total value (like the number 14).

The `\t` combination of characters is an example of an *escape sequence*. Another of Java’s escape sequences, the combination `\n`, moves the cursor to a newline. In other words, `System.out.println("Hello\n")` does the same thing as `System.out.println("Hello").`

# Thinking about Loops (Priming)

I remember when I was a young boy. We lived on Front Street in Philadelphia, near where the El train turned onto Kensington Avenue. Come early morning, I’d have to go outside and get water from the well. I’d pump several times before any water would come out. Ma and Pa called it “priming the pump.”

These days I don’t prime pumps. I prime while loops. Consider the case of a busy network administrator. She needs a program that extracts a username from an e-mail address. For example, the program reads

```
John@BurdBrain.com
```

and writes

```
John
```

How does the program do it? Like other examples in the chapter, this problem involves repetition:

```
Repeatedly do the following:
    Read a character.
    Write the character.
```