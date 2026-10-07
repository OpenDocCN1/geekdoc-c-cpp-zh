# Simple Variables

When you start the program in Listing 3.7, it puts the following text onscreen:

Operation "HyperHype" is now activated!
Enter your agent code: _________

After printing the underscore characters, the program uses the backspace character to back up the cursor to the first underscore.You can enter your secret of code and continue. Here's a complete run:

Operation "HyperHype" is now activated!
Enter your agent code:42007007
You entered 42007007...
Code verified! Proceed with Plan Z3!

# Universal Character Names

C++ implementations support a basic source character set—that is, the set of characters you can write using standard U.S. keyboard, the symbols, as { and =, in the C language, and a scattering of other characters, such as the space character. There is a basic execution character set, which includes characters that can be processed during the execution of a program (for example, characters read from a file or displayed on screen). This adds a few more characters, such as backspace and alert. The C++ Standard also allows implementation to extended source character sets and extended execution character sets. Furthermore, additional characters that qualify as letters can be used as part of the name of an identifier. a German implementation might allow you to use umlauted vowels, and a French implementation might allow accented vowels. C++ has a mechanism for representing international characters that is independent of any particular keyboard: the use of universal character names.

Using universal character names is similar to using sequences. A universal character name begins either with \u or \U. The \u form is followed by 4 hexadecimal digits, and the \U form by 8 hexadecimal digits. These digits represent the ISO 10646 point for the character. (ISO 10646 is an international standard under development that provides numeric codes for a wide range of characters. Use “Unicode and ISO 10646,” in this chapter.)

If your implementation supports extended characters, you can use universal character names in identifiers, as character constants, and in strings. For example, consider the following code:

```
int k\u00F6rper;
cout << "Let eat g\u00E2teau.\\n";
```

The ISO 10646 code point for ö is 00F6, and the code point for å is 00E2. Thus, this C++ code would set the variable name to Körper and display the following output:

Let them eat gâteau.