
- 4. Click OK and then Apply to complete the Extract Method refactoring.

The code you selected in Step 1 is moved to a new method, located below `Main()` and named `OutputInterestTable()`. In the spot that it formerly occupied, you see this method call:

```
principal = OutputInterestTable(principal, interest, duration);
```

The Preview Changes window shows two panes so that you can preview exactly which information will change. The top pane shows the code you’re fixing as it looks now. The lower pane shows the code as it will look when it changes. For more sweeping refactorings, each pane may have numerous lines. You can select or deselect them individually to determine which specific elements to refactor.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_258_0.png)

If, after refactoring, you suffer “buyer’s remorse,” click Undo or press Ctrl+Z.

Suppose that the previous refactoring did something you don’t like, such as fail to include principal as a parameter. (Because this situation is possible, you must always check a refactoring to be certain that it’s what you want.)

This situation happened the first time this section was written, in fact. (I’m writing this chapter based on beta software.) Rather than make principal a parameter, the Extract Method refactoring made it a local variable. To move principal into the parameter list, you can use the Promote Local Variable to Parameter refactoring. But before you do that, you need to initialize the local variable principal (the promotion refactoring doesn’t work if the variable is uninitialized):

```
decimal principal = 0M;   // M means decimal.
```

To carry out the Promote Local Variable to Parameter refactoring, you right-click the local principal variable’s name and click Promote Local Variable to Parameter to move the local variable definition to the parameter list:

```
private static decimal OutputInterestTable(decimal interest,
                                            int duration,
                                            decimal principal) ...
```

However, principal is at the end of the list and you want it at the beginning. You can use the Reorder Parameters refactoring to fix this problem.

To carry out Reorder Parameters, right-click the new principal parameter and click the Reorder Parameters link. In the dialog box, click the principal line to select it. Then click the ↑ button twice to move principal to the top of the list. Click OK.

## Why you should bother with methods

When FORTRAN introduced the function concept — methods, in C# — during the 1950s, its sole purpose was to avoid duplication of code by combining similar sections into a common element. Suppose that you were to write a program to calculate ratios in multiple places. Your program could call the `CalculateRatio()` method when needed, for more or less the sole purpose of avoiding duplicate code. The savings may not seem important for a method as small as `CalculateRatio()`, but methods can grow much larger. Besides, a common method such as `WriteLine()` may be invoked in hundreds of different places.

Quickly, a second advantage became obvious: Coding a single method correctly is easier than coding many — and is doubly easier if the method is small. The `CalculateRatio()` method includes a check to ensure that the denominator isn't zero. If you repeat the calculation code throughout your program, you can easily remember this test in some cases — and in other places, forget.

Not as obvious is a third advantage: A carefully crafted method reduces the complexity of the program. A well-defined method should stand for a concept. You should be able to describe the purpose of the method without using the words *and* or *or*. The method should do only one thing.

A method such as `CalculateSin()` is an ideal example. The programmer who's tasked with this assignment can implement this complex operation with no concern about how it may be used. The applications programmer can use `CalculateSin()` with no concern about how this operation is performed internally, which greatly reduces the number of issues she must monitor. After the number of “variables” is reduced, a large job is accomplished by implementing two smaller, easier jobs.

Large programs, such as word processors, are built up from many layers of methods at ever-increasing levels of abstraction. For example, a `RedisplayDocument()` method would undoubtedly call a `Reparagraph()` method to redisplay the paragraphs within the document. `Reparagraph()` would need to invoke a `CalculateWordWrap()` method to decide where to wrap the lines that make up the paragraph. `CalculateWordWrap()` would have to call a `LookUpWordBreak()` method to decide where to break a word at the end of the line, to make the sentences wrap more naturally. Each of these methods was described in a single, simple sentence. (Notice that these methods are well named.)

Without the ability to abstract concepts, someone writing programs of even moderate complexity would find that the task becomes almost impossible — let alone creating an operating system such as Windows Vista, a utility such as WinZip, a word processor such as WordPerfect, or a game such as *Halo.*

The result of all this refactoring consists of these two pieces:

- A new private static method below `Main()`, named `OutputInterestTable()`
- The following line of code within `Main()` where the extracted code was:

```
principal = OutputInterestTable(principal, interest, duration);
```

Cool! The same divide-and-conquer logic holds for `InputInterestData()`. However, that type of refactoring is more complex, so I do it by hand and don’t show the steps. A description of that sort of refactoring is beyond the scope of this book, though you can find an introduction at csharp102.info. Experiment with the Refactor menu and use it often for building better-factored code. But always check the results.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_260_0.png)

Because C# 4.0 now supports named parameters, you can call the parameters in whatever order you want, by specifying the name of the expected parameter before the value when calling a method. I cover more of this topic later in Book 8, but in C# 4.0, reordering parameters is less of an issue.

For `InputInterestData()`, you can focus solely on inputting the three decimal values. However, in this case, you realize that inputting each one involves identical operations on three different input variables. The `InputPositiveDecimal()` method bundles these operations into a general code that you can apply to principal, interest, and duration alike. Notice that the three while loops that take input in the original program are collapsed into one while loop inside `InputPositiveDecimal()`. This process reduces code duplication.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_260_1.png)

Avoid duplicating code. Refactoring folks call it the worst “code smell.”

This `InputPositiveDecimal()` method displays the prompt it was given and awaits input from the user. The method returns the value to the caller if it isn’t negative. If the value is negative, the method outputs an error message and loops back to try again.

From the user’s standpoint, the modified program acts exactly the same as the inline version, which is just the point:

```
Enter principal:100
Enter interest:-10
Interest cannot be negative
Try again

Enter interest:10
Enter duration:10

Principal     = 100
Interest      = 10%
Duration      = 10 years

1-110.0
2-121.00
3-133.10
4-146.41
5-161.05
6-177.16
7-194.88
8-214.37
9-235.81
10-259.39
Press Enter to terminate...
```

I've refactored a lengthy, somewhat difficult program into smaller, more understandable pieces — while reducing some duplication. As they say in my neck of the woods, “You can’t beat that with a stick.”

## Having Arguments with Methods

A method such as the following example is about as useful as Bill Sempf’s hairbrush because no data passes into or out of the method:

```
public static void Output()
{
    Console.WriteLine("this is a method");
}
```

Compare this example to real-world methods that do something. For example, the mathematical sine operation requires some type of input — after all, you have to calculate the sine of something. Similarly, to concatenate two strings, you need two strings. So the Concatenate() method requires at least two strings as input. (As The Beav might say, “Gee, Wally, that sounds logical.”) You need to find a way to move data into and out of a method.

### Passing an argument to a method

The values you input to a method are method arguments, or parameters. Most methods require some type of arguments if they’re going to do something. (In this way, methods remind me of my son: We need to have an argument before he’ll do anything.) You pass arguments to a method by listing them in the parentheses that follow the method name. Consider this small addition to the earlier Example class:

```
public class Example
{
    public static void Output(string someString)
    {
        Console.WriteLine("Output() was passed the argument: " + someString);
    }
}
```

I could invoke this method from within the same class, like this:
