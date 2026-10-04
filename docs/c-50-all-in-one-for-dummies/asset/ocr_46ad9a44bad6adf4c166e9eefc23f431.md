# # Chapter 4: Transforming Text Templates

In This Chapter

+   - Discovering where templating for Visual Studio originated
- Defining a user case for T4
- Getting your environment ready for T4
- Using T4 like a language

T4 (Text Template Transformation Toolkit) is a code-generation toolkit built into Visual Studio. It is a built-in language used to make the default ASP.NET and Windows Forms files in C# or VB (for example, when you use the Add New Item feature).

> Scott Hanselman, from Microsoft, said it best: "Now’s time to introduce code generation to your company." I wholeheartedly agree. Code generation increases developer productivity, decreases bugs in final versions, and makes people happy.

Lars Cornelius, a Microsoft MVP, said "T4 in VS is the equivalent to index.php in Apache," and he is not far from the truth. T4 is a starting point for a project, providing seamless redirection and logical formatting of what the user (in this case, the developer) actually sees. It is the template, just as its name suggests.

T4 is a big topic, like so many others in this book, but you should be able to get started code generation from the material here. Getting your environment ready and understanding the concepts are the most important steps.

# ## Getting to Know T4

In this chapter, I look at T4 as a code-generation tool. It is a lot more than that. Really, it is a tool for the management of metadata around Domain Specific Languages. If that makes no sense to you, join the club.

Many things about computer science are elegant, and the current drive toward meta-programming and the use of higher and higher level languages to