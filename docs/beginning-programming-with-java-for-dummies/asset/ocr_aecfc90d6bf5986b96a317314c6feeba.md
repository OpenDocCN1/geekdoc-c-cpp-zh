# From Your Mind to the Computer's Processor

When you create a new computer program, you go through a multistep process. The process involves three important tools:

+   ✔ **Compiler:** A compiler translates your code into computer-friendly (human-unfriendly) instructions.
+   ✔ **Virtual machine:** A virtual machine steps through the computer-friendly instructions.
+   ✔ **Application programming interface:** An application programming interface contains useful prewritten code.

The next three sections describe each of the three tools.

# Translating your code

You may have heard that computers deal with zeros and ones. That's certainly true, but what does it mean? Well, for starters, computer circuits don't deal directly with letters of the alphabet. When you see the word Start on your computer screen, the computer stores the word internally as 01010011 01110100 01100001 01110010 01110100. That feeling you get of seeing a friendly looking five-letter word is your interpretation of the computer screen's pixels, and nothing more. Computers break everything down into very low-level, unfriendly sequences of zeros and ones and then put things back together so that humans can deal with the results.

So what happens when you write a computer program? Well, the program has to get translated into zeros and ones. The official name for the translation process is compilation. Without compilation, the computer can't run your program.

I compiled the code in Listing 1-1. Then I did some harmless hacking to help me see the resulting zeros and ones. What I saw was the mishmash in Figure 1-1.

The compiled mumbo jumbo in Figure 1-1 goes by many different names:

+   ✔ Most Java programmers call it bytecode.
+   ✔ I often call it a class file. That's because, in Java, the bytecode gets stored in files named SomethingOrOther.class.
+   ✔ To emphasize the difference, Java programmers call Listing 1-1 the source code and refer to the zeros and ones in Figure 1-1 as object code.