

## Figure 12.1

Abstraction generally allows you to view large sets of tasks in smaller sets.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_319_0.png)

Decomposition involves, among other things, asking a fairly rudimentary question: What is the order of the tasks to be performed? With the designation of an order of tasks comes the designation of dependencies. You know what you need for each task to be fulfilled. In Figure 12.1, for example, it makes little sense to check the spelling if no textual content exists.

Abstraction serves to eliminate dependencies. It accomplishes this feat by encapsulating code. Encapsulation ends up being an enormous asset in most industrial situations. Consider this: If you set up your programs so that the different functions you create are not tangled up with other functions, then you can more easily change one thing in isolation. This is one of the major benefits of encapsulation. Programmers can make isolated changes. The technical terms for this are loosely coupled and highly cohesive. In other words, the code in a function coheres: It makes sense when examined in isolation. A function is also loosely coupled with other functions, meaning that if you make changes to one function, you do not have to make changes in other functions.

## Functional Abstraction in Programs

Figure 12.2 illustrates how you can use decomposition of the functionality to address the project depicted in Figure 12.1. The analysis involves four abstractions. Each abstraction relates to a task or set of tasks the program might perform as it provides the envisioned service. To access information involves in some way obtaining the information from some source. The source might be the program itself, a file containing text, or a database. Organizing information might involve sorting it or being able to select specific items from it. Processing user selections might involve taking input from the terminal. Displaying information might involve working with a DOS character display, creating a window component, or using a browser. In each instance, you can create functions that isolate a specific task so that it can be seen in isolation from others.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_320_0.png)

When you develop a computer program, you can try to create the program as a single flow of activity that proceeds from a beginning to an end. As Figure 12.3 illustrates, in this light, you can decompose the program in terms of the sequence of tasks it performs and the abstractions that identify different segments of the sequence of tasks. In this respect, you have analyzed the program so that it now consists of functional subroutines.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_320_1.png)

## Identifying Functional Subroutines

To create a functional subroutine (from here on referred to as a function) in Perl, you employ a combination of program syntax and convention. The syntax and conventions apply to both the specific development of functions and the broader layout of programs in which you include functions. Table 12.1 provides a summary.

### Table 12.1 Syntax and Conventions for Functions

| Item | Discussion |
|---|---|
| sub | This is a keyword that allows you to designate the word that follows it as the name of a function. |
| Name | Functions have names. The name of a function can be almost any expression you choose. You cannot use words reserved for other purposes in Perl (`continue`, `for`, `while`, and so on). The function name should not be a number or consist of operators or controls. It should begin with an alphabetical character. Function names can include underscores and dashes, among other characters (`A_Za_z0`), but they must always begin with a character and cannot include hyphens. |
| Block | In this context, block refers to a set of curly braces (`{}`). You must enclose the statements that compose the body of the function in curly braces. The curly braces follow the name of the function. |
| return | You can use the `return` keyword with functions. The `return` keyword closes out the function so that you can predict the precise value the function makes available in the flow of the program. The return value allows you to specify the value that the function passes back to the calling code. |
| Arguments | When you create a function, you can define a list of arguments you can pass to the function. You can pass these arguments to the function inside a set of parentheses that follow the name of the function. When you define a function, you can make it clear what arguments the function receives by following a coding standard that identifies the arguments. |
| Program organization | You can organize a program on a structural, package, or modular basis. On a modular basis, you place functions in separate files or groups of files known as modules. If you use a package approach, you divide a single file into separate parts using package labels. If you use a structural approach, you try to place all the code that constitutes a program into functions and then, to set up the program, call the functions. |

## Basic Program Organization for Functions

When you develop functions, you can use any of a number of programming techniques. One that many programmers favor requires that you organize your programs structurally. Structural organization of a program entails placing a program in a file so that you see calls to functions first and then the definitions of the called functions. Figure 12.4 illustrates the practical consequences of this type of organization.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_322_0.png)

Organized structurally, a program hides the details involved in the definition of functions. When you hide details, you make it simpler to understand your code. You likewise make it possible to make repairs to your program without having to become involved in functions other than those you need to fix.

When you define a function, you compose the lines of code that constitute the function. The definition of a function, then, consists of a body of code enclosed in curly braces and preceded by the name of the function and the appropriate keyword (usually sub). In a structurally organized program, as Figure 12.5 illustrates, you employ the top of the program for calling functions. You reserve the remainder of the program for the functions you have developed.

During the development cycle of a program’s life, you can employ the top of the program as a development area. Using this approach, you can have a fairly clear view of the overall program, but as the need arises, you can “open” a functional space and either add to it or create new functionality.

For more involved programs, the structural approach to development still pertains, but rather than placing functions in a submerged area of a single file, you move them to separate files. The separate files become modules or packages. Figure 12.6 illustrates this situation.

When you create a function, you attempt to hide complexity, making the operations the function contains visible to the user of the function only through the calls made to the function. The structural organization of the program accommodates both abstraction and development. It accommodates abstraction because it allows the person who maintains the program to understand it according to the functions it uses. It accommodates development because it allows you to create programs in a staging area at the top of the program, thus avoiding the necessity of digging into what might amount to hundreds or thousands of lines of code that constitute the program.

## Functions with No Arguments

The most fundamental type of function in Perl can be characterized as taking no arguments and providing no return values. Such a function resembles the blocks developed in Chapter 11, with the difference that they can be used more flexibly. Listing12_01 employs functions to replace the opening, menu, and display options. All the functions used employ no arguments and do not explicitly return values.

```perl
#Listing12_01
#Functions without arguments
system('cls');
$NL = "\n" ;
$ML = $NL x 5; #Multiple line returns for displays
```

> Figure 12.5
> The development of the program takes place at the top of the program.

> Figure 12.6
> Programs consisting of multiple files place defined functions in modules or packages.

