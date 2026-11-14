Similarly, we need conditional compilation when we want to use a new language feature that is not available on all target platforms, say, move semantics (§2.3.5):

```
#ifdef MY_LIBRARY_WITH_MOVE_SEMANTICS
... make something efficient with mode
#else
... make something less efficient but portable
#endif
```

Here we can use the feature when available and still keep the portability to compilers without this feature. Of course, we need reliable tools that define the macro only when the feature is really available. Conditional compilation is quite powerful but it has its price: the maintenance of the sources and the testing are more laborious and error-prone. These disadvantages can be lessened by well-designed encapsulation so that the different implementations are used over a common interfaces.

# 1.9.2.4 Nestable Comments

The directive #if can be used to comment out code blocks:

```
#if 0
... Here we wrote pretty evil code! One day we fix it. Seriously.
#endif
```

The advantage over /* ... */ is that it can be nested:

```
#if 0
... Here the nonsense begins.
#if 0
... Here we have nonsense within nonsense.
#endif
... The finale of our nonsense. (Fortunately ignored.)
#endif
```

Nonetheless, this technique should be used with moderation: if three-quarters of the program are comments, we should consider a serious revision.

Recapitulating this chapter, we illustrate the fundamental features of C++ in Appendix A.3. We haven't included it in the main reading track to keep the high pace for the impatient audience. For those not in such a rush we recommend taking the time to read it and to see how non-trivial software evolves.

# 1.10 Exercises

# 1.10.1 Age

Write a program that asks input from the keyboard and prints the result on the screen and writes it to a file. The question is: “What is your age?”