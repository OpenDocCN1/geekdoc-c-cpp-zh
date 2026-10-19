This simple code makes this technique look like a tidy solution, but production code often requires more extensive housekeeping or cleanup when an error condition is detected. Here is a more realistic example:

```
More Realistic Visual Basic Code That Uses Guard Clauses to Clarify the Nominal Case
* set up, bailing out if errors are found
If Not file.validName() Then
    errorStatus = FileError_InvalidFileName
    Exit Sub
End If

If Not file.Open() Then
    errorStatus = FileError_CantOpenFile
    Exit Sub
End If

If Not encryptionKey.valid() Then
    errorStatus = FileError_InvalidEncryptionKey
    Exit Sub
End If

If Not file.Decrypt( encryptionKey ) Then
    errorStatus = FileError_CantDecryptFile
    Exit Sub
End If

* lots of code
...
```

This is the code for the nominal case.

With production-size code, the Exit Sub approach creates a noticeable amount of code before the nominal case is handled. The Exit Sub approach does avoid the deep nesting of the first example, however, and, if the code in the first example were expanded to show setting an errorStatus variable, the Exit Sub approach would do a better job of keeping related statements together. When all the dust settles, the Exit Sub approach does appear more readable and maintainable, just not by a very wide margin.

# Minimize the number of returns in each routine

It’s harder to understand a routine when, reading it at the bottom, you’re unaware of the possibility that it returned somewhere above. For that reason, use returns judiciously—only when they improve readability.

# 17.2 Recursion

In recursion, a routine solves a small part of a problem itself, divides the problem into smaller pieces, and then calls itself to solve each of the smaller pieces. Recursion is usually called into play when a small part of the problem is easy to solve and a large part is easy to decompose into smaller pieces.

Recursion isn’t useful often, but when used judiciously it produces elegant solutions, as in this example in which a sorting algorithm makes excellent use of recursion:

![](bbox=[0.15, 0.85, 0.22, 0.92])