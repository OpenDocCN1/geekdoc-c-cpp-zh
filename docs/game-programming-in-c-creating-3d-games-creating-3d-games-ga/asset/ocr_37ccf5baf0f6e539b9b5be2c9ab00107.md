Luckily, this book sticks to **cross-platform** libraries, meaning that the libraries work on many different platforms. All the source code for this book works on recent versions of both Windows and macOS. Although Linux support is untested, the game projects generally should also work on Linux.

One of the foundational libraries used in this book is Simple DirectMedia Layer (SDL; see https://www.libsdl.org). The SDL library is a cross-platform game development library written in C. It provides support for creating windows, creating basic 2D graphics, processing input, and outputting audio, among other features. SDL is a very lightweight library that works on many platforms, including Microsoft Windows, Apple macOS, Linux, iOS, and Android.

In this first chapter, the only external library needed is SDL. Subsequent chapters use other libraries and introduce them when needed.

# THE GAME LOOP AND GAME CLASS

One of the big differences between a game and any other program is that a game must update many times per second for as long as the program runs. A **game loop** is a loop that controls the overall flow for the entire game program. Like any other loop, a game loop has code it executes on every iteration, and it has a loop condition. For a game loop, you