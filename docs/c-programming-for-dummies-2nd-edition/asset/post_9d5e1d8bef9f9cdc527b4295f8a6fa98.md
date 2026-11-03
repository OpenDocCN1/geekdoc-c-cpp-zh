
**Exercise 9-16:** Type the source code from Listing 9-7 into the editor. Mind your typing! The final *while* statement (refer to Line 16) must end with a semicolon; otherwise, the compiler gets all huffy on you.

Here’s the output:

```
0 1 1 2 3 5 8 13 21 34 55 89 144 233
```

The loop begins at Lines 7 and 8, where the variables are initialized.

Lines 12 through 15 calculate the Fibonacci values. Two *print()* functions display the values.

The loop ends on Line 16, where the *while* statement makes its evaluation. As long as variable `nacci` is less than 300, the loop repeats. You can adjust this value higher to direct the program to output more Fibonacci numbers.

On Line 18, the *putchar()* statement cleans up the output by adding a newline character.

**Exercise 9-17:** Redo your solution to Exercise 9-14 as a *do while* loop.

## Loopy Stuff

I could go on and on about loops all day, repeating myself endlessly! Before moving on, however, I’d like to go over a few looping tips and pitfalls. These things you should know before you get your official *For Dummies* Looping Programmer certificate.

### Looping endlessly

Beware the endless loop!

![](img/dcc0cd79d4a45cfce24fa49d85442884_141_0.png)

When a program enters an endless loop, it either spews output over and over without end or it sits there tight and does nothing. Well, it’s doing what you ordered it to do, which is to spin forever. Sometimes, this setup is done on purpose, but mostly it happens because of programmer error. And with the way loops are set up in C, it’s easy to unintentionally loop *ad infinitum*.

Listing 9-8 illustrates a common endless loop, which is a programming error, not a syntax error.

### LISTING 9-8: A Common Way to Make an Endless Loop

```c
#include <stdio.h>

int main()
{
    int x;
    for(x=0;x=10;x=x+1)
    {
        puts("What are you lookin' at?");
    }
    return(0);
}
```

The problem with the code in Listing 9-8 is that the for statement's exit condition is always true: x=10. Read it again if you didn't catch it the first time, or just do Exercise 9-18.

**Exercise 9-18:** Type the source code for Listing 9-8. Save and build, ignoring any warnings. Run.

The program runs — infinitely.

![](img/dcc0cd79d4a45cfce24fa49d85442884_142_0.png)

- To break out of an endless loop, press Ctrl+C on the keyboard. This trick works only for console programs, and it may not always work. If it doesn't, you need to kill the process run amok, which is something I don't have time to explain in this book.
- Endless loops are also referred to as *infinite loops*.

## Looping endlessly but on purpose

Occasionally, a program needs an endless loop. For example, a microcontroller may load a program that runs as long as the device is on. When you set up such a loop on purpose in C, one of two statements is used:

```c
for(;;)
```

I read this statement as “for ever.” With no items in the parentheses, but still with the required two semicolons, the for loop repeats eternally — even after the cows come home. Here’s the while loop equivalent:

```
while(1)
```

The value in the parentheses doesn’t necessarily need to be 1; any true or non-zero value works. When the loop is endless on purpose, however, most programmers set the value to 1 simply to self-document that they know what’s up.

You can see an example of an endless loop on purpose in the next section.

## Breaking out of a loop

Any loop can be terminated instantly — including endless loops — by using a break statement within the loop’s repeating group of statements. When break is encountered, looping stops and program execution picks up with the next statement after the loop’s final curly bracket. Listing 9-9 demonstrates the process.

### LISTING 9-9: Get Me Outta Here!

```c
#include <stdio.h>

int main()
{
    int count;

    count = 0;
    while(1)
    {
        printf("%d ",count);
        count = count+1;
        if( count > 50)
            break;
    }
    putchar('\n');
    return(0);
}
```

The while loop at Line 8 is configured to go on forever, but the if test at Line 12 can stop it: When the value of count is greater than 50, the break statement (refer to Line 13) is executed and the loop halts.

**Exercise 9-19:** Build and run a new project using the source code from Listing 9-9.

**Exercise 9-20:** Rewrite the source code from Listing 9-9 so that an endless for loop is used instead of an endless while loop.

![](img/dcc0cd79d4a45cfce24fa49d85442884_144_0.png)

You don't need to construct an endless loop to use the break statement. You can break out of any loop. When you do, execution continues with the first statement after the loop's final curly bracket.

## Adding multiple for loop conditions

A common mistake in a for loop is to use commas instead of semicolons to separate the parts. But commas are allowed in the for loop's parentheses, just not to replace the semicolons. Instead, they are used to specify multiple initialization operations as well as multiple looping conditions. Listing 9-10 shows how you can get nutty with commas in a for statement.

### LISTING 9-10: Crowded in Here

```c
#include <stdio.h>

int main()
{
    int a;
    char c;

    for( a=1,c='Z'; a<5; a+=1,c-=1 )
        printf("%d%c\n",a,c);
    return(0);
}
```

Line 8 shows a for statement with two initializations and two expressions that take place each time the loop repeats. Both pairs are separated by a comma. The semicolons still group each of the three parts in a for loop.

First, variable a is initialized to 1 and variable c is initialized to the letter Z. The loop spins as long as the value of variable a is less than 5. And after each statement repeats, the value of variable a is increased by 1 and the value of variable c is decreased by 1.

**Exercise 9-21:** Type the source code from Listing 9-10 into your editor. Build and run.

## Screwing up a loop

I know of two common ways to mess up a loop. These trouble spots crop up for beginners and pros alike. The only way to avoid these spots is to keep a keen eye so that you can spot 'em quick.

The first goof-up is specifying a condition that can never be met; for example:

```
for(x=1;x==10;x=x+1)
```

In the preceding line, the exit condition is false before the loop spins once, so the loop is never executed. This error is almost as insidious as using an assignment operator (a single equal sign) instead of the “is equal to” operator (as just shown).

Another common mistake is misplacing the semicolon, as in

```
for(x=1;x<14;x=x+1);
{
    puts("Sore shoulder surgery");
}
```

Because the first line, the for statement, ends in a semicolon, the line is the entire loop. The empty code repeats 13 times, which is what the for statement dictates. The puts() statement is then executed once.

![](img/dcc0cd79d4a45cfce24fa49d85442884_145_0.png)

Rogue semicolons can be frustrating!

The problem is worse with while loops because the do while structure requires a semicolon after the final while statement. In fact, forgetting that particular semicolon is also a source of woe. For a traditional while loop, you don’t do this:

```
while(x<14);
{
    puts("Sore shoulder surgery");
}
```

Most compilers catch these rogue semicolon issues with a warning. Still, be on the lookout, as Listing 9-11 demonstrates.

### LISTING 9-11: A for Loop with No Body

```c
#include <stdio.h>

int main()
{
    int x;
    for(x=0;x<10;x=x+1,printf("%d\n",x));
    ;
    return(0);
}
```

In the example shown in Listing 9-11, the semicolon is placed on the line after the for statement at Line 8. This location shows deliberate intent.

As with the example from the preceding section, two expressions are placed in the for statement’s parentheses, both separated by a comma.

**Exercise 9-22:** Type the source code from Listing 9-11 into your editor. Build and run.

Though you can load up items in a for statement's parentheses, it's rare and not recommended for readability's sake.

## AVOID GOTO HELL

The third looping statement is the most despised and the lowest-of-the-low C language keywords. It's goto, which is pronounced "go to" not "got-to." It directs program execution to another line in the source code, a line tagged by label. Here's an example:

```
here:
puts("This is a type of loop");
goto here;
```

As this chunk of code executes (from the top down), the here label is ignored. The puts() function comes next, and, finally, goto redirects program flow back up to the here label. Everything repeats. Everything works. But it's just darn ugly.

Most clever programmers can craft their code in ways that don't require goto. The result is something more readable — and that's the key. Code that contains lots of goto statements can be difficult to follow, leading experienced programmers to describe it as spaghetti code. The goto statement encourages sloppy habits.

The only time goto might truly be necessary is when busting out of a nested loop. Even in this situation, an example would be contrived. So it's probably safe to say that you'll run your entire programming career and, hopefully, never have to deal with a goto statement in C.
