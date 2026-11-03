# Streaming Input Restrictions

The basic input and output functions in the C language aren't interactive. They work on streams, which are continuous flows of input or output, interrupted only by an end-of-file marker or, occasionally, the newline character.

When you plan to read only one character from input, be aware that the Enter key, pressed to process input, is still waiting to be read from the stream. A second input function, such as another getchar(), immediately fetches the Enter key press (the \n character). It does not wait, as an interactive input function would.

![](bbox=[0.13, 0.42, 0.2, 0.52])

+   - If you desire interactive programs, get a library with interactive functions, such as the NCurses library. You can check out my book on Ncurses, available from Amazon.com in the kindle eBook and printed formats.
+   - The end-of-file marker is represented by the EOF constant, defined in the stdio.h header file.
+   - The newline character is represented by the \n escape sequence.
+   - The newline character's ASCII value may differ from machine to machine, so always specify the escape sequence \n for the newline.

![](bbox=[0.13, 0.58, 0.2, 0.68])