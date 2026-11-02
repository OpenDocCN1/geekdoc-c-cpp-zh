So change just one character in a Java program and instead of an uneventful compilation, you get a big headache! Change p to P like so:

```
//The following line is incorrect:
System.out.Println(keyboard.nextLine());
```

When you type the program in Eclipse's editor, you get the ugliness shown in Figure 5-6.

Figure 5-6
The Java compiler understands println, but not Println.

![](bbox=[0.2, 0.38, 0.55, 0.65])

When you see error markers and quick fixes like the ones in Figure 5-6, your best bet is to stay calm and read the messages carefully. Sometimes, the messages contain useful hints. (Of course, sometimes they don't.) The message in Figure 5-6 is The method Println(String) is undefined for the type PrintStream. In plain English, this means "The Java compiler can't interpret the word Println." (The message stops short of saying, "Don't type the word Println, you Dummy!" In any case, if the computer says you're one of us Dummies, you should take it as a compliment.) Now, there are plenty of reasons why the compiler may not be able to understand a word like Println. But, for a beginning programmer, you should check two important things right away:

+   ✓ Have you spelled the word correctly?
+     Did you accidentally type println (with a digit 1) instead of println?
+   ✓ Have you capitalized all letters correctly?
+     Did you incorrectly type Println or PrintLn instead of println?

Either of these errors can send the Java compiler into a tailspin. So compare your typing with the approved typing word for word (and letter for letter). When you find a discrepancy, go back to the editor and fix the problem. Then try compiling the program again.