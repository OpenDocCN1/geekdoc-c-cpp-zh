(continued)

> But wait! To grab a single character from the keyboard, I call findWithinHorizon(".", 0).charAt(0). What's the role of charAt(0) in reading a single character? Unfortunately, any findWithinHorizon call behaves as though it's finding a bunch of characters, not just a single character. Even when you call findWithinHorizon(".", 0), and the computer fetches just one letter from the keyboard, the Java program treats that letter as one of possibly many input characters.
> 
> The call to charAt(0) takes care of the multicharacter problem. This charAt(0) call tells Java to pick the initial character from any of the characters that findWithinHorizon fetches.
> 
> Yes, it's complicated. And yes, I don't like having to explain it. But no, you don't have to understand any of the details in this sidebar. Just read the details if you want to read them and skip the details if you don't care.

I wish I could give you 12 simple rules to help you decide when and when not to reuse variables. The problem is, I can't. It all depends on what you're trying to accomplish. So how do you figure out on your own when and when not to reuse variables? Like the guy says to the fellow who asks how to get to Carnegie Hall, "Practice, practice, practice."

# Reading characters

The people who created Java's Scanner class didn't create a next method for reading a single character. So to input a single character, I paste two Java API methods together. I use the findWithinHorizon and charAt methods.

Table 5-1 in Chapter 5 introduces this findWithinHorizon(".", 0).charAt(0) technique for reading a single input character, and Listing 8-3 uses the technique to read one character at a time. (In fact, Listing 8-3 uses the technique four times to read four individual characters.)

Notice the format for the input in Figure 8-5. To enter the characters in the word pots, I type four letters, one after another, with no blank spaces between the letters and no quote marks. The findWithinHorizon(".", 0).charAt(0) technique works that way, but don't blame me or my technique. Other developers' character-reading methods work the same way. No matter whose methods you use, reading a character differs from reading a number. Here's how:

> With methods like nextDouble and nextInt, you type blank spaces between numbers.
> 
> If I type 80 6, then two calls to nextInt read the number 80, followed by the number 6. If I type 806, then a single call to nextInt reads the number 806 (eight hundred six), as illustrated in Figure 8-8.