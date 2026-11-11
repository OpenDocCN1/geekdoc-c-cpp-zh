
## Accessing data

To access a particular element, we use square brackets again, containing the index of the element we want. So `x[0]` means the first element in an array named `x`. If we just say `x` with no brackets, we're referring to the whole array.

```
my_second_array = [2, 5, 6, 8]
print(my_second_array[0])
>> 2
```

> Now just print out the first element — remember, array indexes start at 0!

> Let's change the second value (so index of 1).

```
my_second_array[1] = 3
print(my_second_array)
>> [2, 3, 6, 8]
```

> And now, let's print the whole array!

You can do lots of neat things with an array, like check how many elements it has, rearrange the order, add elements to it or take them out. If you do take an element out then all the ones after it move up, like taking a carriage out of the middle of a train.

![](img/862cb7d96d05319b069165a3aaaaa9d3_38_0.png)

![](img/862cb7d96d05319b069165a3aaaaa9d3_39_0.png)

## The world's first computer programmer

![](img/862cb7d96d05319b069165a3aaaaa9d3_39_1.png)

Meet Ada. Ada Lovelace, born in 1815, was the world's first computer programmer. This would be impressive enough, but she lived at a time when women weren't expected to tackle anything much more complicated than embroidery. And to top it all off, she did all this a century before anyone actually built a computer...

Daughter of the famous (and scandalous) poet Lord Byron, Ada was taught maths and science in an attempt to keep her from following in her father's badly behaved footsteps, and she fell in love with the subjects. At 17 she met a man who would change her life: Charles Babbage.

![](img/862cb7d96d05319b069165a3aaaaa9d3_39_2.png)

### The Difference Engine

Babbage was an engineer, astronomer and inventor. Being an astronomer back then involved doing a lot of sums, and Babbage wanted to make a machine to do them for him: a machine would never get bored and wouldn't make mistakes.

This was the 1820s, though. There were no computer chips, no transistors, not even any electricity. But that didn't stop Babbage. His machine would be made of nothing more than cogs, gears and other mechanisms. He named it the Difference Engine.

Babbage spent 20 years and huge sums of government money on the project, but the technology of the time just wasn't up to the challenge, and he could never get the machine to work.

When Ada met Charles, he told her about a new idea of his. It was an even more complicated machine, the Analytical Engine, which could do any sort of calculations. This was the first time anyone had thought of a computer. Ada was fascinated by the whole idea, and helped Babbage figure out how it could work. By doing so she became the first person to ever work out how to program a computer. The Analytical Engine was never made either, but that didn't stop Ada figuring out how to use it. And while Babbage was still thinking in terms of doing simple mathematics, she foresaw that one day computers would do amazing things, even composing music!

### That's neat!

Ada never saw a real computer, but modern engineers have named a programming language, Ada, after her.

### The Analytical Engine

![](img/862cb7d96d05319b069165a3aaaaa9d3_40_0.png)

## Making Things Functional

So far all the program examples you've seen have been of a single set of instructions, executed in order. However, all but the simplest programs rely on functions: blocks of code split out that can be called from other places in the program. Functions let you write code in manageable chunks, and save you from copy/pasting code if you need to do the same thing in different places.

![](img/862cb7d96d05319b069165a3aaaaa9d3_41_0.png)

### Getting into a function

Function definitions often start with a keyword that varies from programming language to language, like *function* or *def*. Then your function needs a unique name (which, like a variable, can't contain any spaces). After the name comes a set of brackets that can contain a number of arguments. These are variables that are passed into your function that you can then use inside it. Finally, you add some curly brackets. These define the code block that gets run as part of the function.

You can call a function from anywhere in the code by writing the name of the function followed by a pair of brackets containing the same number of variables as in the function definition. You'll notice this looks like calling the *print* statement. That's because print is a function defined by the language itself, that works just like the ones you can define.

> Variables declared in an argument or inside the code block are scoped to that block: they don't exist outside it. This means you don't need to worry about reusing variable names; so long as you don't reuse them within the same block you're fine.

### Getting out of a function

Your code block can contain any code you like, plus a new, special statement: `return`. When the program reaches a `return` statement it immediately exits the function and jumps back to the line it was called from without executing the rest of the function code. If you just put `return` it will jump back on its own. If you put `return` and then a variable or value it will return with that value. If the code reaches the end of the function without hitting a `return` statement it will return without any value.

```python
function calculate_square(my_var)
{
  result = my_var*my_var
  return result
}

var = calculate_square(3)
var = calculate_square(var)
print(var)
>> 81
```

- defining a function with one argument
- return the 'result' variable
- call the function passing in '3' as the argument
- call it again on the result

## Coding Tools

![](img/862cb7d96d05319b069165a3aaaaa9d3_43_0.png)

In the end program code is just text, so you can write it in any text editor you like. However, over the years, developers have come up with a range of tools to make writing code easier.

### A smarter text editor

Some text editors are designed for writing code. One very useful trick they have is to change the text colour to separate out variables, statements and other things. They'll also make strings stand out, which is very handy when you forget the closing quote on a string and it ends up going on forever ...

These editors need to understand the programming language you're using to do these tricks; most will support many common languages. Some can detect it automatically from what you write or from the extension of the filename (py for Python, for example); others will have an option in the menu to set it.

These little tweaks may not sound like much but actually they make reading and writing code far easier – once you've tried it you'll never go back to a boring old black-and-white editor!

![](img/862cb7d96d05319b069165a3aaaaa9d3_43_1.png)

### IDEs

An IDE, or integrated development environment, looks like a text editor on the surface but is much more powerful. As well as smart colour coding an IDE will have a play button to build and run your program directly, and will often be able to find and organise all your functions. They may even have more complex tools like debuggers built into them. IDEs are much more complex than a text editor and are not as straightforward to set up and start using. They also need to be configured for each language you are using, and some may only support one particular programming language. While just about every programmer uses a smart text editor of some kind, not all use an IDE; you should start out with a text editor and then try an IDE later to see how useful you find it.

### Coding in your browser

These days the internet has sites that will let you write, run and experiment with code for a number of different languages right in your browser. This is a fantastic way to jump straight in and start writing some simple programs without needing to install anything on your computer.

![](img/862cb7d96d05319b069165a3aaaaa9d3_44_0.png)

![](img/862cb7d96d05319b069165a3aaaaa9d3_44_1.png)
