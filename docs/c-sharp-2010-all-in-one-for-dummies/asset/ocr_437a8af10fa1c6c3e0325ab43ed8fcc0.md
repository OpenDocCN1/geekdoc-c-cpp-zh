![](bbox=[0.18, 0.13, 0.35, 0.52])

Figure 4-5:
The generated code file.

# Using Some of the T4 Directives

Clearly this is a very Hello World example. The magic of T4 is complex, and I had to spend a lot of time (believe it or not) making the simplest example.

One of the things that makes T4 work well are the directives built into the language. These commands are just like shell commands. They have parameters and perform certain tasks on the file.

# Setting the output

The first directive you see in the example in the earlier section "Creating a template from a text file" is the output directive. I wanted a C# file, so I used the .cs extension. You could emit anything, though — text, HTML, VB, or even a custom format that you need for your project, such as

```
<#@ output extension=".bill" #>
```

Another parameter for output is Encoding, which is exactly what it sounds like. Options include

+   ♦ Default
+   ♦ ASCII