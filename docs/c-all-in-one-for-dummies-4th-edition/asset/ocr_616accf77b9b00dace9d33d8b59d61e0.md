+   4. Read an individual stock entry from the file.
+   5. Put the data into the Stock object.
+   6. Close the file.

Here are a couple of reasons to close a file after you’ve finished using it:

+   - **Other applications might be waiting to use the file.** Some operating systems allow an application to *lock* a file, meaning that no other applications can open the file while the application that locked the file is using it. In such situations, another application can use the file after you close it, but not until then.
+   - **When you write to a file, the operating system decides whether to immediately write the information onto the hard drive or flash drive/SD card or to hold on to it and gather more information, finally writing it all as a single batch.** When you close a file, the operating system puts all your remaining data into the file. This is called *flushing* the file.

You have two ways to write to a file:

+   - **Sequential access:** In sequential access, you write to a file or read from a file from beginning to end. With this approach, when you open the file, you normally specify whether you plan to read from or write to the file, but not both at the same time. After you open the file, if you’re writing to the file, the data you write gets added continually to the end of the file. Or if you’re reading from the file, you read the data at the beginning, and then you read the data that follows, and so on, up to the end.
+   - **Random access:** With random access, you can read and write to any byte in a file, regardless of which byte you previously read or wrote. In other words, you can skip around. You can read some bytes and then move to another portion of the file and write some bytes, and then move elsewhere and write some more.

Back in the days of the C programming language, several library functions let you work with files. However, they stunk. They were cumbersome and made life difficult. So, when C++ came along, people quickly created a set of classes that made life with files much easier. These people used the stream metaphor we’ve been raving about. In the sections that follow, you discover how to open files, write to them, read from them, and close them.

Filing Information with the Streams Library