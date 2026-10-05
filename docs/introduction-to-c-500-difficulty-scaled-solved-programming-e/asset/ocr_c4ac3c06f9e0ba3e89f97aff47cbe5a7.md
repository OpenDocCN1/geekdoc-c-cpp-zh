# Introduction to C++

know what you intend to do. Therefore, a successful compilation does not mean that your program would operate as you expect. I write this again, especially for novice programmers. If your program is compiled it does not mean that it will work as you want. For example, if you want to write some code that displays the Less if the variable a is less than 5, and you write:

```
if (a > 5)
    cout << "Less\n";
```

then, although these lines will be compiled successfully, the code will not display Less. This type of error is a logical error (bug) not detected by the compiler. The use of the word bug as a synonym of programming is credited to the mathematician and scientist Grace Hopper, when she discovered a hidden bug inside her computer caused its abnormal operation.

If the program does not operate as you expect, you are in trouble. The depth of trouble you are depends on the size of the code. If it extends to hundreds of lines, you'll probably find the logical errors in a short time and the debugging process won't take long. But if your program consists of thousands of lines, the debugging may become time-consuming, painful, and very stressful, particularly if your supervisor hangs over your head demanding immediate results. To avoid such situations, always remember my advice: try to write simple, clear, readable, and maintainable code.

# READING THIS BOOK

As for the linguistic expressions of this book, I'd say there is nothing special. If some code is marked as program behaviour is undefined, then means the program may continue to run, crash, or produce unexpected results. All scenarios are possible. What is the most likely scenario? According to Murphy's Law, to work normally during the development phase and crash when you perform a public demonstration. Also, if your program works with a compiler it may fail while reading with another or with a different version of the compiler. So, what might cause undefined behaviour.

If some code is marked as result depends on the implementation or it is platform dependent, it means that if you compile your program with another compiler or transfer it to another system and code, it may produce different results. As you can imagine, debugging a program that runs normally on one system and not another is very process. If you want your program to be portable, do not write code that depends on the system which you are using.

In my experience, the first step to learn a programming language is through coding exercises. You'll find many examples throughout this book. Some are just snippets, while others are complete programs that help you understand the material. After understanding (and not reading) a topic, the next step is to write code to test your knowledge. You cannot learn a programming language by just reading it; you must write your code. For reason, each chapter provides many programming exercises. A program may be written in several ways. When reading an exercise, my advice is to hide the answer and write your own version. Then compare the solutions. Pay extra attention to all types of question “What is the output of the following program?” Each chapter ends with a number of unsolved exercises for more practice. Always try to test your skills and understanding of what you've learned, before continuing to the next chapter. Remember, to learn any programming language, you must write your programs and experiment with them; that, is the only way.

C++ is a powerful language with many features, rules, and concepts. So, don't be disappointed if some text or examples in this book make it difficult for you to understand. It is normal to feel that way. The best way to overcome difficulties is to write, simple programs and experiment with them so that you gradually become familiar with the features of the language and how they work.

Oh, almost forgot, as you “heard” in our first program, you'll need a pair of speakers ...