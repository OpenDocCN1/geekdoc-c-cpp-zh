Example 2-3 shows examples of integral variable declarations.

# EXAMPLE 2.3

```
int studentCount; // number of students in the class
int ageOfStudent = 20; // age - originally initialized to 20
int numberOfExams; // number of exams
int coursesEnrolled; // number of courses enrolled
```

> NOTE
> 
> Notice that each declaration ends with a semicolon (;). This is because variable declarations are considered statements in the C# language. All statements end in a semicolon.

In Example 2-3, identifiers are chosen that adhere to the rules listed for naming program items. Every line also contains an inline comment. These comments are unnecessary because the identifiers are self-documenting. If nondescriptive identifiers, such as x, y, or s, are used, comments would be helpful.

> NOTE
> 
> Do not place a comment on every line or with every variable declaration because it creates unreadable code. It is best to include comments when a segment of code needs further explanation.

Each identifier in Example 2-3 consists of two or more words. The second and subsequent words begin with an uppercase character. This naming convention is used throughout the textbook for variable and object names. The first character of the identifier begins with a lowercase character.

Class and method names, both user-defined and Framework class library (FCL) class identifiers, begin with an uppercase character. Constants, which are covered later in this chapter, are named with all uppercase characters, using the underline character to separate words. This is the standard style used by C# programmers.

> NOTE
> 
> Style is composed of a set of personal choices adopted by programmers. If you are new to programming, you might want to follow the textbook's style for selecting identifiers; however, your instructors might have different styles that they recommend. Another common naming convention is to separate words with an underscore. The most important thing to remember is that after selecting a style, you should use it consistently.