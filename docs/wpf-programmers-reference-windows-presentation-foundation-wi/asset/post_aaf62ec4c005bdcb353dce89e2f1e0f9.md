
# INTRODUCTION

For decades, good developers have separated UI construction from the code behind the user interface. Keeping the two separate makes it easier to distribute work among different developers and makes it easier to build each piece separately. WPF continues this philosophy by making the separation between the user interface and the code behind more distinct than ever.

In fact, Microsoft's original vision was that specialized graphic designers built the user interface, and programmers added the code behind completely.

While many development projects cannot afford separate graphic designers and programmers, it's still worthwhile to keep these two tasks separate. This book specifically addresses those who perform either of those tasks.

This book provides an introduction to WPF and does not require that you have any experience with it. In fact, it doesn't require you to have any previous programming or UI design experience.

> I don't want to receive a bunch of flaming e-mails complaining that some of the material is too basic, so I'm warning you right now! If you're mortally offended by introductory material, you're welcome to skip the first few chapters and move on to the more advanced material.

Although this book does not require previous programming experience, it covers a lot of material and gets into some advanced topics. By the time you finish reading it, you should have learned a lot no matter how experienced you are at the start.

# WHAT THIS BOOK COVERS (AND WHAT IT DOESN'T)

This book explains WPF development. It explains how to build user interfaces using Microsoft's Expression Blend tool, Visual Studio, and the XAML programming language. It also explains how to use Visual Studio to attach code to the interface.

WPF is a very flexible tool, and you can use it to make amazing user interfaces. Unfortunately, it is also often complicated, occasionally confusing, and sometimes daunting. You can use it to perform remarkable feats of UI sleight-of-hand, but doing so can be a heroic adventure in experimentation and browsing.

Such deeds of development fly in the face of Microsoft's vision that specialized graphic designers build user interfaces that programmers then attach to code. I'm hanging out with the wrong crowd, but the designers I've met did not have the skills or interest to spend time constructing elaborate UI interfaces. Instead, they wanted to focus on the interface's appearance and usability.

This book's philosophy is that the user interface is a front end to the application, not the application itself. It should not take years of experience and a PhD in WPF to build a data entry form.

If it takes a huge assortment of sneaky tricks to make a program perform some esoteric stunt, this book doesn't cover it. For more complex situations, the book will freely jump between the user interface and how code behind it. For example, if a particular animation is hard to control with pure WPF but easy to control using code behind the scenes, I'll opt for the option every time.

This book also doesn't cover programming the interface. It demonstrates some of the code that you can learn how to write your own code, but it doesn't cover C#, Visual Basic, or any other programming language in detail.

# HOW THIS BOOK IS STRUCTURED

The chapters in this book are generally arranged from the most basic in the beginning to the more advanced at the end. They start with fundamentals such as adding controls to windows and selecting the kinds of controls to use. Later chapters cover more advanced techniques as animation, transformations, and 3D graphics. The appendices provide a handy reference for controls and other objects, and XAML syntax.

The book will probably make the most sense if you read the chapters in order, then you can skip around a bit if you need information on a particular topic. For example, after you read the first chapters and how to build simple WPF applications, you might want to skip and read a bit more about styles or transformations.

If you have developed experience, particularly with Expression Blend or Visual Studio, you may want to skip the earliest chapters.

If you know you will not be using Expression Blend or Visual Studio, you may want to skip the corresponding chapters. For example, if you know that you will be using Visual Studio and not Expression Blend, then you may want to skip Chapter 3.

- Chapter 1: WPF Overview — Chapter 1 covers basic WPF concepts. It explains WPF's advantages, how WPF is layered on top of DirectX, and how WPF separates UI design from the code behind it. It also describes the different kinds of WPF projects (stand-alone, XAP, library) and explains Page, Frame, and PageFunction projects in general terms.

- Chapter 2: WPF in Visual Studio — Chapter 2 explains how to build WPF projects with Visual Studio. It tells how to build a simple user interface and how to connect interfaces with the code behind them. This chapter explains how to control properties and how to edit XAML code in Visual Studio. It does not explain WPF controls in great depth because they are covered.

- Chapter 3: Expression Blend — Chapter 3 explains how to build WPF projects with Expression Blend. It tells you how to edit XAML code in Expression Blend and how to link to Visual Studio to add code behind.

- Chapter 4: Common Properties — Chapter 4 describes some properties that are common to many WPF controls. These properties define basic control features such as color, size, and position.

- Chapter 5: Content Controls — Chapter 5 describes WPF's controls that are intended to display content (as opposed to the controls described in the following chapters). These include controls such as Label, GroupBox, ListBox, and Image. This chapter describes the purpose of each control and summarizes its most important properties and behaviors.

- Chapter 6: Layout Controls — Chapter 6 describes WPF controls that are intended to arrange other controls. These include controls such as Grid, DockPanel, StackPanel, and WrapPanel. This chapter describes the purpose of each control and summarizes its most important properties and behaviors.

- Chapter 7: User Interaction — Chapter 7 describes WPF controls that are intended to allow the user to control the application. These include controls as as Button, RadioButton, TextBox, and Slider. This chapter describes the purpose of each control and summarizes its most important properties and behaviors.

- Chapter 8: Two-Dimensional Drawing Controls — Chapter 8 describes WPF objects that perform two-dimensional (2D) drawing. These include Line, Ellipse, Rectangle, Polygon, Polyline, and Path. This chapter also explains the Path mini-language and geometries, which can create multiple drawings.

- Chapter 9: Properties — Chapter 9 explains WPF properties in detail. Whereas the earlier chapters use them to provide simple examples, this chapter describes properties in greater depth. It explains basic properties as simple text, properties that can be entered as multiple values, properties that are objects, dependency properties, and attached properties.

- Chapter 10: Pens and Brushes — Chapter 10 describes the pen and brush objects that you use to determine the graphical appearance of WPF objects. In addition to simple-color pens and brushes, this chapter describes more complex objects as dashed pens, gradients, and image brushes.

- Chapter 11: Events and Code-Behind — Chapter 11 explains routed events, tunneling (preview), bubbling, and attached events. These different kinds of events allow you to use a user interface that was created with WPF to change the code behind the scene.

- Chapter 12: Resources — Chapter 12 explains WPF resources. It tells how to use static and dynamic resources in XAML code.

- Chapter 13: Styles and Property Triggers — Chapter 13 explains styles and property triggers. It tells how to use styles, usually stored as resources, to give objects a consistent appearance. (For example, see Figure 0–4.) It also explains property triggers, which are often defined in styles, to change a control's appearance when a property value changes.

- Chapter 14: Event Triggers and Animation — Chapter 14 explains event triggers and the animations they can run. It explains storylines and timelines that WPF applications perform with little effort.

- Chapter 15: Templates — Chapter 15 describes control templates. It explains how you can use templates to change the appearance and behavior of predefined controls. It also tells how to use ItemsPresenter and ContentPresenter objects to change the ways lists and menus work.
