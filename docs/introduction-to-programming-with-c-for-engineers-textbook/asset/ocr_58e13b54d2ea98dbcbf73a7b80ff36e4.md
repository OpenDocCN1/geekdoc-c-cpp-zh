![](bbox=[0.137, 0.101, 0.851, 0.485])

**Figure 2.10** The Coliru online compiler environment (http://coliru.stacked-crooked.com) running in the Mozilla Firefox viewer with the code from Listing 2.3 copied and pasted into the editor pane. Under it is the output pane. The lower-left pane contains the command line to build and run the program. At lower right are the action buttons.

We obtain the following output:

```
a b c d e f g h i j k l m n o p q r s t u v w x y z

2 0 3 1 4 1 2 2 3 0 0 1 0 4 3 0 0 1 2 2 1 1 0 0 2 0
```

That is, each letter is associated with the frequency of its occurrence in the input sentence.

# 2.6.3 Histogram Code, Explained

Let’s now split up the code from Listing 2.3 and explain what it does, line by line. On lines [1–3], `#include <file_name>` is called, where *file_name* corresponds to a header file. As alluded to earlier, headers contain already-written code that we can use to simplify our lives as programmers. Figuring out what header to choose for a given language component is sometimes difficult—the easiest way is to look it up on the Internet. Here we include *iostream* for the `std::cout` and `std::cin` objects, which represent the screen and the keyboard, respectively. Then the *string* file is introduced, to use the `std::string` class to store plain text. Finally, a *vector* that contains the definition of the `std::vector` class that allows us to store the histogram is included, as shown in Figure 2.9.