# Developing with Style 675

have everything merged together. It just makes things easier to keep track of.

+   **Speed and security:** Using this pattern, Microsoft compiles the C# code into a DLL, just like the class libraries Book II delves into. This makes the application much faster and protects the application somewhat from criminals.

+   **Legacy-based:** This pattern mimics Windows Forms development, going back to Visual Basic 3. It is easy for people to pick up if they already have experience. I know that history isn't always the best to mimic, but it can't hurt.

# Building in n-tier

Going the opposite direction from inline code, I have used to be called n-tier code, but now it's a hundred different things. At the essence here, I am talking about purposely dividing the code of the application up to DLLs, instead of just Having Studio do it for you.

Book VI
Chapter 2
Building
Applications Web

To show what I mean in pictures. Figure 2-7 shows a normal code-behind style ASP.NET application. Now, say you put all the data access code — that talks to the database — in one class project. Then you put all the business logic — math and validation stuff — in another class project.

```
HTML/ASP.NET Markup
```

```
C# view-specific code
```

```
C# business-specific code
```

**Figure 2-7:**nStructure of
n-tier code.

```
C# data-specific code
```

All the code in the code-behind markup work, right? That's the idea. Layering your application like this makes debugging easier, separates concerns even more, and provides for code reuse. It's also easier to unit test. If you have a cellphone application that uses the same data model, then you can use the same database code if you break it out.