# LISTING 1-6 A for loop

```
C# version
for (int i=0; i<=100; i++)

F# versions
// for loop with i from 0 to 100
for i=0 to 100 do ...

// for iterate the element in list 0 to 100
for i in [0..100] do ...

for...downto sample
// downto go from 100 to 0
for i=100 downto 0 do ...
```

> Note [0..100] defines a list with elements from 0 to 100. The details about how to define a list are discussed later in this book.

Some readers might immediately ask how to make the for../downto increase or decrease by 2. for../downto does not support this, so you will have to use for..in with a sequence or list. And I can assure you, you will not use for for loop that often when you understand how to use a sequence or list.

# while Loops

Another approach could be used to accomplish the goal of this example is to use a while loop. F# and C# approach the while loop in the same way. Listing 1-7 shows an example.

# LISTING 1-7 A while loop

```
C# version
int i = 0;
while (i<=100)
{
    // your operations
    i++;\}
```