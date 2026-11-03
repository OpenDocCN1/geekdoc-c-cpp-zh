
## IN THIS CHAPTER
- Maintain good posture
- Use creative names
- Write functions when needed
- Work on your code a little bit at a time
- Break apart larger projects into several modules
- Know what a pointer is
- Use whitespace before condensing
- Know when if-else becomes switch-case
- Remember to use assignment operators
- When you get stuck, read your code aloud

## Chapter 27
### Ten Reminders and Suggestions

It’s difficult to narrow down the list of reminders and suggestions, especially for a topic as rich and diverse as programming. For example, I could suggest ways to fit in with other programmers, which movies to quote, which games to play, and even which foods to eat. A programming subculture exists — even today, though the emphasis on professional workplace attire has thankfully abated.

Beyond social suggestions, I do have a few things to remind you of — plus, some general-purpose C language recommendations. Believe it or not, every programmer has been through the same things you've experienced. It's good to hear advice from a grizzled programming veteran.

### Maintain Good Posture

I'm certain that some authority figure somewhere in your early life drilled into you the importance of having proper posture. Ignore them at your own peril, especially when you're young and haven't yet gotten out of bed to say, "Ouch."

For many programmers, coding becomes an obsession. As an example, it's quite easy for me to sit and write code for many hours straight. Such a stationary position is hard on the body. So, every few minutes, take a break. If you can't manage that, schedule a break. Seriously: The next time you compile, stand up! Look outside! Walk around a bit!

While you're working, try as hard as you can to keep your shoulders back and your wrists elevated. Don't crook your neck when you look at the monitor. Don't hunch over the keyboard. Look out a window to change your focus.

![](img/dcc0cd79d4a45cfce24fa49d85442884_419_0.png)

I might also add that it's pleasant to acknowledge others. True, it's easy to grunt or snarl at someone when you're in the midst of a project. Keep in mind that other humans may not appreciate the depth of thought and elation you feel when you code. If you can't be pleasant now, apologize later.

### Use Creative Names

The best code I've seen reads like a human language. It's tough to make the entire source code read that way, but for small snippets, having appropriate variable and function names is a boon to writing clear code.

For example, the following expression is one of my favorites:

```
while(!done)
```

I read this statement as "while not done." It makes sense. Until the value of the done variable is TRUE, the loop spins. But somewhere inside the loop, when the exit condition is met, the value of done is set equal to TRUE and the loop stops. It's lucid.

It also helps to offer descriptive names to your functions. A name such as setringervolume() is great, but the name set_ringer_volume() is better. It also helps to consider the function in context. For example:

```
ch=read_next_character();
```

In the preceding line, the function read_next_character() needs no explanation — unless it doesn't actually return the next character.

### Write a Function

Anytime you use code more than once, consider throwing it off into a function, even if the code is only one line long or appears in several spots and doesn't really seem function-worthy.

Suppose that you use the fgets() function to read a string, but then you follow fgets() with another function that removes the final newline character from the input buffer. Why not make both items their own function, something like get_input()?

### Work on Your Code a Little Bit at a Time

A majority of the time you spend coding is to fix problems, to correct flaws in logic, or to fine-tune. When making such adjustments, avoid the temptation to make three or four changes at one time. Address issues one at a time.

The reason for my admonition is that it's tempting to hop around your code and work on several things at a time. For example: You need to fix the spacing in a printf() statement's output, adjust a loop, and set a new maximum value. Do those things one at a time!

When you attempt to do several things at a time, you can screw up. But which thing did you goof up? You have to go back and check everything, including the related statements and functions, to ensure that they work. During situations like these, you will seriously wish for a time machine. Instead, just work on your code a little bit at a time.

### Break Apart Larger Projects into Several Modules

No one likes to scroll through 500 lines of code. Unless you're totally immersed in your project and can keep everything stored in your noggin, break out functions into modules.

I prefer to group related functions into similar files. I typically have an output file, an input file, an initialization file, and so on. Each file, or module, is compiled and linked separately to form the code. The benefits are that the files are smaller and if they compile and work, you no longer need to mess with them.

### Know What a Pointer Is

A pointer is a variable that stores a memory location. It’s not magic, and it shouldn’t be confusing, as long as you keep the basic mantra in your head:

A pointer is a variable that stores a memory location.

A memory location stored in a pointer references another variable or a buffer (like an array). Therefore, the pointer must be initialized before it’s used:

A pointer must be initialized before it’s used.

When the pointer variable is prefixed by the * (asterisk) operator, it references the contents of the variable at the memory location. This duality is weird, of course, but it’s highly useful, as demonstrated in Chapters 18 and 19.

- Declare a pointer variable by using the * prefix.
- Use the & operator to grab the address of any variable in C.
- Arrays are automatically referenced by their memory locations, so you can use an array name without the & prefix to grab its address.
- "Address" and "memory location" are the same thing.
- A great way to explore pointers is to use the Code::Blocks debugger; specifically, the Watches window. See Chapter 25.

![](img/dcc0cd79d4a45cfce24fa49d85442884_421_0.png)

### Add Whitespace before Condensing

C programmers love to bunch up statements, cramming as many of them as they can into a single line. Even I am guilty of this pleasure, as shown by a few examples from this book, such as

```c
while(putchar(*(sample++)))
```

Admit it: Such a construction looks cool. It makes it seem like you really know how to code C. But it can also be a source of woe.

My advice: Split out the code before you condense it. Make liberal use of whitespace, especially when you first write the code. For example, the line

```c
if( c != '\0' )
```

is easier to read than the line

```c
if(c!='\0')
```

After you write your code with whitespace — or use several statements to express something — you can condense, move out the spaces, or do whatever else you like.

![](img/dcc0cd79d4a45cfce24fa49d85442884_422_0.png)

In C language source code, whitespace is for the benefit of human eyes. I admire programmers who prefer to use whitespace over cramming their code onto one line, despite how interesting it looks.

### Know When if-else Becomes switch-case

I'm a big fan of the if-else decision tree, but I generally avoid stacking up multiple if statements. To me, it usually means that my programming logic is flawed. For example:

```c
if(something)
;
else if(something_else)
;
else(finally)
;
```

This structure is okay, and it's often necessary to deal with a 3-part decision. But the following structure, which I've seen built by many budding C programmers, probably isn't the best way to code a decision tree:

```c
if(something)
;
else if(something_else_1)
;
else if(something_else_2)
;
else if(something_else_3)
;
else if(something_else_4)
;
else if(finally)
;
```

Generally speaking, anytime you have that many else-if statements, you probably need to employ the switch-case structure instead. In fact, my guess is that this example is probably what inspired the switch-case structure in the first place.

See Chapter 8 for more information on switch-case.

### Remember Assignment Operators

Though it's nice to write readable code, one handy tool in the C language is an assignment operator. Even if you don't use one, you need to be able to recognize it.

The following equation is quite common in programming:

```c
a = a + n;
```

In C, you can abbreviate this statement by using an assignment operator:

```c
a += n;
```

![](img/dcc0cd79d4a45cfce24fa49d85442884_423_0.png)

The operator goes before the equal sign. If it went afterward, it might change into a unary operator, which looks weird:

```c
a =+ n;
```
