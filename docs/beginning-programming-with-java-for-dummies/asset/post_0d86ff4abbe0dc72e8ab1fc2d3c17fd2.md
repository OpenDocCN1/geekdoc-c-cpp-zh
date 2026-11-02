
## Be patient.

Every good programming effort takes a long time to get right. If you don't understand something right away, be persistent. Stick with it (or put it away for a while and come back to it). There's nothing you can't understand if you put in enough time.

## Don't become frustrated.

Don't throw your pie crust. Frustration (not lack of knowledge) is your enemy. If you're frustrated, you can't accomplish anything.

## Don't think you're the only person who's slow to understand.

I'm slow, and I'm proud of it. (Melba, Chapter 6 will be a week late.)

## Don't be timid.

If your code isn't working and you can't figure out why it's not working, then ask someone. Post a message on an online forum. And don't be afraid of anyone's snide or sarcastic answer. (For a list of gestures you can make in response to peoples' snobby answers, see Appendix Z.)

To ask me directly, send me an e-mail message, tweet me, or post to me on Facebook. (Send e-mail to BeginProg@allmycode.com, tweets to @allmycode, or posts to Facebook at /allmycode.)

## Diagnosing a problem

The "Typing and running a program" section, earlier in this chapter, tells you how to run the EchoLine program. If all goes well, your screen ends up looking like the one shown in Figure 5-1. But things don't always go well. Sometimes your finger slips, inserting a typo into your program. Sometimes you ignore one of the details in Listing 5-1, and you get a nasty error message.

Of course, some things in Listing 5-1 are okay to change. Not every word in Listing 5-1 is cast in stone. So here's a nasty wrinkle — I can't tell you that you must always retype Listing 5-1 exactly as it appears. Some changes are okay; others are not. Keep reading for some "finstances."

## Case sensitivity

Java is case-sensitive. Among other things, case-sensitive means that, in a Java program, the letter P isn't the same as the letter p. If you send me some fan mail and start with "Dear barry" instead of "Dear Barry," I still know what you mean. But Java doesn't work that way. So change just one character in a Java program and instead of an uneventful compilation, you get a big headache! Change p to P like so:

```
//The following line is incorrect:
System.out.Println(keyboard.nextLine());
```

When you type the program in Eclipse's editor, you get the ugliness shown in Figure 5-6.

Figure 5-6
The Java compiler understands println, but not Println.

![](img/f938eba5f15e231d828a6255e7ec5523_124_0.png)

When you see error markers and quick fixes like the ones in Figure 5-6, your best bet is to stay calm and read the messages carefully. Sometimes, the messages contain useful hints. (Of course, sometimes they don't.) The message in Figure 5-6 is The method Println(String) is undefined for the type PrintStream. In plain English, this means "The Java compiler can't interpret the word Println." (The message stops short of saying, "Don't type the word Println, you Dummy!" In any case, if the computer says you're one of us Dummies, you should take it as a compliment.) Now, there are plenty of reasons why the compiler may not be able to understand a word like Println. But, for a beginning programmer, you should check two important things right away:

- ✓ Have you spelled the word correctly?
  - Did you accidentally type print1n (with a digit 1) instead of println?
- ✓ Have you capitalized all letters correctly?
  - Did you incorrectly type Println or PrintLn instead of println?

Either of these errors can send the Java compiler into a tailspin. So compare your typing with the approved typing word for word (and letter for letter). When you find a discrepancy, go back to the editor and fix the problem. Then try compiling the program again.

![](img/f938eba5f15e231d828a6255e7ec5523_125_0.png)

As you type a program in Eclipse's editor, Eclipse tries to compile the program. When Eclipse finds a compile-time error, the editor usually displays at least three red error markers (see Figure 5-6). The marker in the editor's left margin has an X-like marking and sometimes a tiny light bulb. The marker in the right margin is a small rectangle. The marker in the middle is a jagged red underline.

If you hover your mouse over any of these markers, Eclipse displays a message that attempts to describe the nature of the error. If you hover over the jagged line, Eclipse displays a message and possibly a list of suggested solutions. (Each suggested solution is called a quick fix.) If you right-click the left margin's marker (or control-click on a Mac) and choose Quick Fix in the resulting context menu, Eclipse displays the suggested solutions. To have Eclipse modify your code automatically (using a suggestion from the quick-fix list), either single-click or double-click the item in the quick-fix list. (That is, single-click anything that looks like a link; double-click anything that doesn't look like a link.)

## Omitting punctuation

In English and in Java, using the proper punctuation is important.

Take, for example, the semicolons in Listing 5-1. What happens if you forget to type a semicolon?

```
//The following code is incorrect:
    System.out.println(keyboard.nextLine())
}
```

If you leave off the semicolon, you get the message shown in Figure 5-7.

![](img/f938eba5f15e231d828a6255e7ec5523_125_1.png)

A message like the one in Figure 5-8 makes your life much simpler. I don't have to explain the message, and you don't have to puzzle over the message's meaning. Just take the message insert ";" to complete Statement on its face value. Insert the semicolon between the end of the System.out.println(keyboard.nextLine()) statement and whatever code comes after the statement. (For code that's easier to read and understand, tack on the semicolon at the end of the System.out.println(keyboard.nextLine()) statement.)

Figure 5-8: An unwanted semicolon messes things up.

![](img/f938eba5f15e231d828a6255e7ec5523_126_0.png)

## *Using too much punctuation*

In junior high school, my English teacher said I should use a comma whenever I would normally pause for a breath. This advice doesn't work well during allergy season, when my sentences have more commas in them than words. Even as a paid author, I have trouble deciding where the commas should go, so I often add extra commas for good measure. This makes more work for my copy editor, Melba, who has a trash can full of commas by the desk in her office.

It's the same way in a Java program. You can get carried away with punctuation. Consider, for example, the main method header in Listing 5-1. This line is a dangerous curve for novice programmers.

For information on the terms method header and method body, refer to Chapter 4.

## Why can't the computer fix it?

How often do you get to finish someone else's sentence? "Please," says your supervisor, "go over there and connect the . . ." "Wires," you say. "I'll connect the wires." If you know what someone means to say, why wait for them to say it? This same question comes up in connection with computer error messages. Take a look at the message in Figure 5-7. The computer expects a semicolon after the statement on line 8. Well, Mr. Computer, if you know where you want a semicolon, then just add the semicolon and be done with it. Why are you bothering me about it?

The answer is simple. The computer isn't interested in taking any chances. What if you don't really want a semicolon after the statement on line 8? What if the missing semicolon represents a more profound problem? If the computer added the extra semicolon, it could potentially do more harm than good. Returning to you and your supervisor . . . Boom! A big explosion. "Not the wires, you Dummy. The dots. I wanted you to connect the dots." "Sorry," you say.

Normally, you shouldn't be ending a method header with a semicolon. But people add semicolons anyway. (Maybe, in some subtle way, a method header looks like it should end with a semicolon.)

```
//The following line is incorrect:
public static void main(String args[]); {
```

If you add this extraneous semicolon to the code in Listing 5-1, you get the message shown in Figure 5-8.

The error message and quick fixes in Figure 5-8 are a bit misleading. The message starts with This method requires a body. But the method has a body. Doesn't it?

When the computer tries to compile public static void main(String args[]); (ending with a semicolon), the computer gets confused. I illustrate the confusion in Figure 5-9. Your eye sees an extra semicolon, but the computer's eye interprets this as a method without a body. So that's the error message — the computer says This method requires a body instead of a semicolon.

Figure 5-9: What's on this computer's mind?

![](img/f938eba5f15e231d828a6255e7ec5523_127_0.png)
