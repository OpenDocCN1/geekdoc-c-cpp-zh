# Debugging Your Project

Because computer programming can be a complex process, it's easy to make mistakes. You can introduce errors to your code in a number of ways. Here are two:

+   - Syntax errors are errors in the grammar of your code that make Xcode unable to interpret the code. Typographical mistakes in your code may lead to syntax errors in your project.
- Runtime errors have nothing to do with the syntax of your code. Rather, the logic of your code contains errors that produce an application that doesn't function properly. These mistakes might be syntactically correct and still allow Xcode to compile and link your code into an application, yet produce unexpected or incorrect results. The application may run and even work as expected sometimes, but at some point, your application will do something wrong. A purple apple might be displayed instead of a red one in your graphics application, an enemy invader won't die when shot in your video game, or a miscalculation yields an incorrect numerical result in your spreadsheet application.

The only way to know if you have any bugs in your code is to thoroughly test your projects. When you debug a project, you build, run, and test your application until you're convinced it's bug.

To begin debugging, follow these steps:

+   1. Build and run the project you've been working with throughout this chapter.
2. Type values in the two number fields and then click the Calculate button.
3. Change the numbers and click the Calculate button again.
4. Repeat Step 3 until you're convinced that the project operates as it should.

For example, three consecutive tests of the project yield the following results:

```
1 + 2 = 3
3.25 + 4.75 = 7.999998099265137
3.2 + 4.75 = 7.949998099265137
```

Uh oh! That last test didn' produce results that you might expect. What's going on here? There seem to be three problems: