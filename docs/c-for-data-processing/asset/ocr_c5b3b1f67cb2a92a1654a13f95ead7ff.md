Seasoned programmers break down a problem into a number of smaller ones and make a method for each.

# # Describing the Solution

The actual instructions which describe your solution to the problem must also be part of your program. A single, simple, instruction to do something in a C# program is called a *statement*. A statement is an instruction to perform one particular operation, for example add two numbers together and store the result.

The really gripping thing about programs is that some statements can change which statement is performed next, so that your program can look at things and decide what to do. In the case of C# you can lump statements together to form a lump of program which does one particular task. Such a lump is called a *method*.

A method can be very small, or very large. It can return a value which may or may not be of interest. It can have any name you like, and your program can contain as many methods as you see fit. One method may refer to others. The C# language also has a huge number of *libraries* available which you can use. These save you from "re-inventing the wheel" each time you write a program. We will look at methods in detail later in these notes.

# ## Identifiers and Keywords

You give a name to each method that you create, and you try to make the name of the function fit what it does, for example ShowMenu or SaveToFile. The C# language actually runs your program by looking for a method with a special name, Main. This method is called when your program starts running, and when Main finishes, your program ends. The names that you invent to identify things are called *identifiers*. You also create identifiers when you make things to hold values; woodLength might be a good choice when we want to hold the length of wood required. Later on we will look at the rules and conventions which you must observe when you create identifiers.

The words which are part of the C# language itself are called *keywords*. In a recipe a keyword would be something like "mix" or "heat" or "stir". They would tell you say things like: *heat sugar until molten* or *mix until smooth*. In fact, you'll find that programs look a lot like recipes. Keywords will appear blue in some of the listings in this text.

# ## Objects

Some of the things in the programs that we write are objects that are part of the framework we are using. To continue our cooking analogy, these are things like mixing bowls and ovens, which are used during the cooking process. The names of objects will be given in a different colour, or blue in some of the listings in this text.

# ## Text in a Computer Program

There are two kinds of text in your program. There are the instructions that you want the computer to perform and there are the messages that you want the program to actually display in front of the user. Your mum might add the following instruction to her cake recipe:

> > Now write the words "Happy Christmas" on top of the cake in pink icing.

She is using double quote characters to mark the text that is to be drawn on the cake, and C# works in exactly the same way. "Happy Christmas" is not part of the instructions; it is what needs to be written. These kinds of messages are coloured red in this text.

# ## Colours and Conventions

The colours that I use in this text are intended to line up with the colours you will see when you edit your programs using a professional program editor such as the one supplied as part of Visual Studio. The colours just serve to make the programs easier to understand, and do not have any special meaning. They are added automatically by the editor as you write your program.