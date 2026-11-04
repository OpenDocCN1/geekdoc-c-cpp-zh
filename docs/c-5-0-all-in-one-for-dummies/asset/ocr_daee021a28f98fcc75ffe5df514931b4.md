+   - Polymorphism refers to the general ability to decide which method to invoke at runtime.
+   - Late binding refers to the specific way a language implements polymorphism.

Polymorphism is the key to the power of object-oriented (OO) programming. It's so important that languages that don't support it can't advertise themselves as OO languages. (I think it's an FDA regulation: You can't label a language that doesn't support it as OO unless you add a disclaimer from the surgeon general, or something like that.)

![](bbox=[0.1, 0.38, 0.22, 0.52])

Languages that support classes but not polymorphism are object-based languages. Visual Basic 6.0 (not VB.NET) is an example of such a language.

Without polymorphism, inheritance has little meaning. Let me spring another example on you to show you why. Suppose that you had written a boffo program that uses a class named (just to pick a name out of the air) Student. After months of design, coding, and testing, you release this application to rave reviews from colleagues and critics alike. (You've even heard talk of starting a new Nobel Prize category for software, but you modestly brush such talk aside.)

Time passes, and your boss asks you to add to this program the capability of handling graduate students, who are similar but not identical to undergraduate students. (The graduate students probably claim that they aren't similar in any way.) Suppose that the formula for calculating the tuition amount for a graduate student is completely different from the formula for an undergrad. Now, your boss doesn't know or care that, deep within the program, are numerous calls to the member method CalcTuition(). (A lot of things happen that your boss doesn't know or care about, by the way.) The following example shows one of those many calls to CalcTuition():

```
void SomeMethod(Student s) // Could be grad or undergrad
{
    // . . . whatever it might do . . .
    s.CalcTuition();
    // . . . continues on . . .
}
```

If C# didn't support late binding, you would need to edit someMethod() to check whether the student object passed to it is a GraduateStudent or a Student. The program would call Student.CalcTuition() when s is a Student and GraduateStudent.CalcTuition() when it's a graduate student.

Editing someMethod() doesn't seem so bad, except for two problems: