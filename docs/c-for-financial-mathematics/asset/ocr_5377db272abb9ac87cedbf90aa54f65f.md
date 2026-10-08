So one tiny error can look like a disaster. This is why you should only ever try and fix one error at a time.

You should treat the error messages as the compiler’s best guess of what you’ve got wrong. As the examples above show it can get both the line numbers wrong and the description of the error wrong.

In particular the line number might be slightly below the actual line containing an error, or if you are really unlucky it might think the error is in a different file. The line numbers reported as containing errors actually mark the points where it *realised* that there was an error. This is why they are often below where the real error occurred.

If the compiler tells you that the error is not in your code but in a library it has definitely go it wrong!

You will find it very hard to work out where you have made an error in your code. So always write programs a couple of lines at a time, constantly testing that they compile and run. Then you *know* that any error that appears must be in the lines you’ve just written.

If you made the mistake of writing an enormous chunk of code and can’t work out where the errors are, then delete it all (or comment it out) and put it back piece by piece. Learn from your mistake and start writing code a little bit at a time.

# ### 1.5 Configuring the compiler

We have given a detailed recipe for how to configure the compiler to run a simple program. If you are working on Windows, you will see that there are many available options that we are ignoring. Similarly on Unix our Makefile sets some basic compiler options, but other options are available.

We won’t worry much about configuring the compiler in this book as it is an advanced topic which only becomes important if you are building large programs that use different libraries or if you want to make sure the code is fully optimised.

We have chosen to configure the compiler so that if errors occur when the program is running, the error messages should be a bit more helpful. We call this “debug mode”. Alternatively is also possible to configure the compiler so that it runs as fast as possible. When developing code, or when learning programming for the first time, it is a good idea to prioritise helpful error messages. Once you are happy with your code, you might want to compile it again with different settings so that it runs more quickly. This final version of your code is called the “release” version of your code because it is the version you would release to any users.