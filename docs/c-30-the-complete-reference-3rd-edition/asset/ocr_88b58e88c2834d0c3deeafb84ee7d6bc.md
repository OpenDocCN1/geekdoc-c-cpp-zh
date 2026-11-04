Text is inherited from **Control**.

Next is the `Main()` method, which is declared much like the `Main()` methods found throughout the rest of this book. It is the method at which program execution begins. Notice, however, that it is preceded by the `STAThread` attribute. As a general rule, the `Main()` method of a Windows program should have this attribute. It sets the threading model for the program to a single-threaded apartment (STA). (A discussion of threading models and apartments is beyond the scope of this chapter, but briefly, a Windows application can use one of two different threading models: single-threaded apartment or multithreaded apartment.)

Inside `Main()`, a **WinSkel** object called `skel` is created. Then, the static method `Application.EnableVisualStyles()` is called. This method enables visual styles (themes) if the operating system supports it. It's not technically necessary in a Windows Forms application, but should be used because it enables better looking controls. It should be the first method called by `Main()`. The **Application** class is defined within **System.Windows.Forms**, and it encapsulates aspects common to all Windows applications.

Next, `skel` is passed to the `Run()` method, which is another method defined by the **Application** class, as shown here:

```
```
Application.Run(skel);
```
```

This starts the window running. The `Run()` method used by the skeleton is shown here:

```
```
public static void Run(Form form)
```
```

It takes a reference to a form as a parameter. Since **WinSkel** inherits **Form**, an object of type **WinSkel** can be passed to `Run()`.

When the program is run, it creates the window shown in Figure 26-1. The window has the default size and is fully functional. It can be resized, moved, minimized, maximized, and closed. Thus, the basic features needed by nearly all windows were achieved by writing only a few lines of form-based code. In contrast, the same program written using the C language and directly calling the Windows API would have required approximately five times as many lines of code!

The preceding skeleton defines the outline that most form-based Windows applications will take. In general, to create a form, you create a class that inherits **Form**. Initialize the form to meet your needs, create an object of your derived class, and then call **Application.Run()** on that object.

# ## Compiling the Windows Skeleton

You can compile a Windows program using either the command-line compiler or Visual Studio. For the very short programs shown in this chapter, the command-line compiler is the easiest way; but for real applications, you will probably want to use the IDE. (Also, as explained at the start of this chapter, you will probably want to use the design tools provided by Visual Studio, but that is not the approach described here.) Each way is shown here.

# ### Compiling from the Command Line

Assuming that you call the skeleton **WinSkel.cs**, then to compile the skeleton from the command line, use this command:

```
```
csc /t:winexe WinSkel.cs
```
```

The `/t:winexe` switch tells the compiler to create a Windows application rather than a console program. To run the program, simply enter **WinSkel** at the command line.