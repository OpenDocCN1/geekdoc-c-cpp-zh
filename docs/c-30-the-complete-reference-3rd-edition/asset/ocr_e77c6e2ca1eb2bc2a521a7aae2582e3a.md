string array passed to Main(). The length of the args array will be equal to the number of command-line arguments, which might be zero.

For example, the following program displays all of the command-line arguments that it is called with:

```
// Display all command-line information.
using System;
class CLDemo {
    static void Main(string[] args) {
        Console.WriteLine("There are " + args.Length +
            " command-line arguments.");
        Console.WriteLine("They are:");
        for(int i=0; i < args.Length; i++)
            Console.WriteLine(args[i]);
    }
}
```

If CLDemo is executed like this:

```
CLDemo one two three
```

you will see the following output:

```
There are 3 command-line arguments.
They are:
one
two
three
```

To understand the way that command-line arguments can be used, consider the next program. It uses a simple substitution cipher to encode or decode messages. The message to be encoded or decoded is specified on the command line. The cipher is very simple: To encode a word, each letter is incremented by 1. Thus, A becomes B, and so on. To decode, each letter is decremented. Of course, such a cipher is of no practical value, being trivially easy to break. But it does provide an enjoyable pastime for children.

```
// Encode or decode a message using a simple substitution cipher.
using System;
class Cipher {
    static int Main(string[] args) {
        // See if arguments are present.
        if(args.Length < 2) {
            Console.WriteLine("Usage: encode/decode word1 [word2...wordN]");
            return 1; // return failure code
        }
        // If args present, first arg must be encode or decode.
```