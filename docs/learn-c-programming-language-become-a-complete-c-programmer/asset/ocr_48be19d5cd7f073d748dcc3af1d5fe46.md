and performance?
The use of C++ has changed dramatically over the years and so has the language itself. From the point of view of a programmer, most of the changes have been improvements. The current ISO standard C++ (ISO/IEC 14882-2011, usually called C++11) is simply a far better tool for writing quality software than were previous versions. How is it a better tool? What kinds of programming styles and techniques does modern C++ support? What language and standard-library features support those techniques? What are the basic building blocks of elegant, correct, maintainable, and efficient C++ code? Those are the key questions answered by this book. Many answers are not the same as you would find with 1985, 1995, or 2005 vintage C++: progress happens.
C++ is a general-purpose programming language emphasizing the design and use of type-rich, lightweight abstractions. It is particularly suited for resource-constrained applications, such as those found in software infrastructures. C++ rewards the programmer who takes the time to master

# vi Preface

techniques for writing quality code. C++ is a language for someone who takes the task of programming seriously. Our civilization depends critically on software; it had better be quality software.

There are billions of lines of C++ deployed. This puts a premium on stability, so 1985 and 1995 C++ code still works and will continue to work for decades. However, for all applications, you can do better with modern C++; if you stick to older styles, you will be writing lower-quality and worse-performing code. The emphasis on stability also implies that standards-conforming code you write today will still work a couple of decades from now. All code in this book conforms to the 2011 ISO C++ standard.

This book is aimed at three audiences:

+   - C++ programmers who want to know what the latest ISO C++ standard has to offer,
+   - C programmers who wonder what C++ provides beyond C, and
+   - People with a background in application languages, such as Java, C#, Python, and Ruby,

looking for something “closer to the machine” – something more flexible, something offering better compile-time checking, or something offering better performance.
Naturally, these three groups are not disjoint – a professional software developer masters more than just one programming language.

This book assumes that its readers are programmers. If you ask, “What’s a for-loop?” or “What’s a compiler?” then this book is not (yet) for you; instead, I recommend my Programming:

Principles and Practice Using C++ to get started with programming and C++.
Furthermore, I assume that readers have some maturity as software developers. If you ask “Why bother testing?” or say, “All languages are basically the same; just show me the syntax” or are confident that there is a single language that is ideal for every task, this is not the book for you.
What features does C++11 offer over and above C++98? A machine model suitable for