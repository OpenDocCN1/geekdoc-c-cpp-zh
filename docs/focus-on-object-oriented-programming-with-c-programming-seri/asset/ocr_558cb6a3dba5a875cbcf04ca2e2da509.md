```
Print this third.
Print this last.
```

Note: For the sake of learning some important elements of C++ output streams, we're going to focus our attention of the output from the older C++ compilers.

Obviously, bad.cpp doesn't produce the output we'd expect. Instead of executing its lines in order, the program appears to call the printf() lines first, then the cout lines. Actually, bad.cpp does executes its lines of code properly. The problem is that bad.cpp uses buffered output for cout. When cout (or any ostream object) uses buffered output, cout doesn't display what you send until its output buffer is full or until the buffer is flushed. The two lines in bad.cpp that use cout don't fill the output buffer, and therefore the program doesn't output those strings until it flushes the cout stream when it terminates. Knowing this, we can follow through bad.cpp's code and see what's happening.

First, bad.cpp calls printf() to display the string Print this first., which it immediately displays. Next, bad.cpp inserts the string Print this second. into cout. Since that string doesn't fill cout's buffer, it simply stores the string in memory to display later. Next, bad.cpp calls printf() with the string Print this third., which it immediately displays even though Print this Second. is still in cout's buffer. Finally, bad.cpp inserts the string Print this last. into cout, which cout also stores in memory for later output. When bad.cpp terminates, it calls the destructor for cout, which automatically flushes any non-empty buffers. At this point, the program displays the two strings it inserted into cout.

Fortunately, there is a way you can force cout to flush the contents of its buffer every time you insert some output. (Note that the ability to flush a buffer's output is a very important task in working with output streams.) The ostream class defines the flush() member function, which you can call whenever you'd like. The ostream class also defines the flush manipulator, which you can insert along with other data in the output stream. The following program ok1.cpp uses the flush manipulator to force the display of the strings it inserts into cout.