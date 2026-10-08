# CHAPTER 16: HANDLING EXCEPTIONS IN C#

A problem that arises during the execution of a program is called as an exception. Exceptions provide a way to transfer control from one part of a program to another. In C# exception handling is built on four keywords: catch, try, throw and finally.

+   - Catch- An exception handler catches an exception at a place where you want to handle the problem. The keyword catch indicates the catching of an exception.
- Try – A block of code for which particular exceptions is activated is identified by a try block. It is followed by one more catch blocks.
- Throw – When a problem shows up a program throws an exception and this is done using the throw keyword.
- Finally – It is used to execute a given set of statements, irrespective of the fact whether an exception is thrown or not. For example- if you open a file, then it must be closed whether an exception is raised or not.

# Syntax

Let us assume a block raises an exception, and a method catches an exception using a combination of catch and try keywords. A catch/try block is placed around the code that might generate an exception. The code within the catch/try block is referred to as a protected code, and the syntax for that is as follows –

```
try
{
    // statements causing exception
}
catch (ExceptionName e1)
{
    // error handling code
```