int value, so that if r is a Roman_int, we can write cout << "Roman" << r << " equals " << r.as_int() << "\n";.

+   7. Make a version of the calculator from Chapter 7 that accepts Roman numerals rather than the usual Arabic ones, for example, XXl + CIV == CXXV.

+   8. Write a program that accepts two file names and produces a new file that is the contents of the first file followed by the contents of the second; that is, the program concatenates the two files.

+   9. Write a program that takes two files containing sorted whitespace-separated words and merges them, preserving order.

+   10. Add a command from x to the calculator from Chapter 7 that makes it take input from a file x. Add a command to y to the calculator that makes it write its output (both standard output and error output) to file y. Write a collection of test cases based on ideas from §7.3 and use that to test the calculator. Discuss how you would use these commands for testing.

+   11. Write a program that produces the sum of all the whitespace-separated integers in a text file. For example, bears: 17 elephants 9 end should output 26.

# Postscript

Much of computing involves moving lots of data from one place to another, for example, copying text from a file to a screen or moving music from a computer onto an MP3 player. Often, some transformation of the data is needed on the way. The iostream library is a way of handling many such tasks where the data can be seen as a sequence (a stream) of values. Input and output can be a surprisingly large part of common programming tasks. This is partly because we (or our programs) need a lot of data and partly because the point where data enters a system is a place where lots of errors can happen. So, we must try to keep our I/O simple and try to minimize the chances that bad data “slips through” into our system.