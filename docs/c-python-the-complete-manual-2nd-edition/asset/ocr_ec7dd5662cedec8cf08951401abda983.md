# How to Set Up C++ in Windows

# STEP 5

Next choose an install location for the Code::Blocks files. It’s your choice, but the default will generally suffice, unless of course you have any special requirements. When you click Next, the install begins; when it’s finished a notification pops up asking you if you want to start Code::Blocks now, so click Yes.

![](bbox=[0.065, 0.19, 0.49, 0.35])

# STEP 6

The first time Code::Blocks loads it runs an auto-detect for any C++ compilers you may already have installed on you system. If you don’t have any, click on the first detected option, GNU GCC Compiler, and click the Default button to set it as the system’s C++ compiler. Click OK when you’re ready to continue.

![](bbox=[0.065, 0.45, 0.49, 0.61])

# STEP 7

When the program starts another message appears, informing you that Code::Blocks is currently not the default application for C++ files. You a couple of options: to leave everything as it is or allow Code::Blocks to associate all C++ file types. Again, we would recommend you opt for the last choice to associate Code::Blocks with every supported file type.

![](bbox=[0.065, 0.71, 0.49, 0.86])

# STEP 8

Before you start using Code::Blocks it’s worth explaining exactly why you need the added compiler. First, a compiler is a separate program that reads through your C++ code and checks it against the latest acceptable programming standards; this is why you need the most recently available compiler. This is currently C++17, with C++20 underway.

![](bbox=[0.51, 0.2, 0.93, 0.35])

# STEP 9

Essentially, computers work and understand only binary, ones and zeros, or Machine Language. Programming in binary isn’t effective for human beings. For example, to output the words “Hello World!” to the screen in C++ would appear in binary as:

```
01100011 01101111 01110101 01110100 00100000 01101111 00111100 01010000 00100010 01001000
01100101 01101100 01101100 01101111 00100000
01010111 01101111 01110010 01101100 01100100
00100001 00100010 00111011
```

![](bbox=[0.51, 0.51, 0.93, 0.61])

# STEP 10

The compiler therefore takes what you’ve entered as C++ code and translates that to Machine Language. To execute C++ code the IDE ‘builds’ the code, checking for errors, then pass it through the compiler to check standardisation and convert it to ones and zeros for the computer to act upon. It’s rather clever stuff, when you stop to think about it.

![](bbox=[0.51, 0.71, 0.93, 0.86])