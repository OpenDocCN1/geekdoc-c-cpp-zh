
**Figure 1.9**

Apple’s developer centers are open to everyone. Free entry-level registration offers access to the combined Mac and iPhone SDK.

![](img/2b293e29fc15b0797f113b85dd429b6e_37_0.png)

## Working with Xcode and Interface Builder

Xcode, shown in Figure 1.10, is a complete suite of development tools; it is described in more detail in Chapter 3. In addition to an editor and compiler, it also includes Interface Builder (IB), shown in Figure 1.11.

At first sight IB — as it’s often known — looks like an interface design tool. In fact, the name is misleading. When you create an application, you can use IB to list the objects it loads as it starts. Visible objects appear in the interface, but you can also load data objects that don’t appear there. In reality, Interface Builder is an object hierarchy editor that can also design interfaces, and you can use it to define the entire architecture of your application.

**Figure 1.10**

The Mac and iPhone SDK are built around the Xcode code editor and compiler. Xcode can be used in a simple one-click-to-build way by beginners, or it can be customized and extended almost indefinitely by more experienced developers.

![](img/2b293e29fc15b0797f113b85dd429b6e_38_0.png)

## Working with Safari

Apple also offers the free Safari Developer Program for Web applications. On the Mac and PC, Safari remains a minority interest for now. On the iPhone, you can use Web-app technology to create Web-based apps that have many of the features of conventional iPhone apps but are simpler to create and can be sold directly from a Web site. With HTML5 and CSS3 (Cascading Style Sheets 3) due soon in Safari and other browsers, Web apps are likely to have an interesting future. The Safari development tools also include a powerful JavaScript debugger that you can use in other projects. Although this book isn't about Safari, it can be worth exploring the Safari environment as a halfway house between JavaScript and Flash Web development and the more complex challenges of Objective-C and Cocoa.

**Figure 1.11**

Interface Builder includes a complete list of objects that you can add to an application. It also includes an object hierarchy view, an interface preview, and an Inspector window used to display and edit objects and their settings.

![](img/2b293e29fc15b0797f113b85dd429b6e_39_0.png)

# Summary

This chapter introduced the history of Smalltalk and Objective-C and explained how the development process that created Cocoa began with Smalltalk, moved to Objective-C and NeXTStep, and culminated in the integration of the Cocoa libraries into Mac OS with the release of OS X.

It also explored various commercial business models for iPhone and OS X development, and it introduced the Apple Developer Program and the Xcode SDK.

![](img/2b293e29fc15b0797f113b85dd429b6e_40_0.png)

# Think Cocoa!

![](img/2b293e29fc15b0797f113b85dd429b6e_40_1.png)

Although it’s possible to learn Cocoa by rote, laboriously listing its objects and trying to memorize their key properties and code interfaces, Cocoa comes alive when you understand its design principles in a more open way. Some of these principles derive from Objective-C. Others are related to Aqua — the OS X look and feel built on top of Cocoa — and are described in more detail later in this chapter. It’s much easier to master Cocoa by understanding its design philosophy and filling in coding details, as needed, than by working backward from Cocoa code examples.

## Designing for Cocoa

Apple products emphasize creative design; a successful design includes the following three elements:

- **Outstanding aesthetics.** Applications should look inspiring and attractive, and users should feel curious and fascinated as soon as they see the interface. But design should enhance features without overpowering them.

- **A sense of fun and creative possibility.** This element isn’t always appropriate — for example, it’s not usually emphasized in office applications — but even the simplest or most straightforward applications can include elements that inspire users.

![](img/2b293e29fc15b0797f113b85dd429b6e_40_2.png)

> **TIP**
> 
> Applications sometimes try to fake fun and creativity by including templates and canned content. This can be popular with users, but it’s more rewarding — and more difficult — to create an application that empowers users to be completely original.

- **A clean and intuitive mental model.** Users should be able to understand the application’s features with as little conscious effort as possible. The application should be invisible; users should never have to think about how to perform an operation.

| In This Chapter |
| --- |
| Designing with Cocoa |
| Creating Cocoa applications |
| Moving to Cocoa and Objective-C from other platforms |

![](img/2b293e29fc15b0797f113b85dd429b6e_40_3.png)

> **CAUTION**
> 
> Users may have many ideas about how features should work. A clean and intuitive mental model can still fail if it doesn’t match those expectations. For example, users sometimes find iTunes difficult because they assume that an iPod can work as an external USB drive. As a model, an external drive is simpler than the way iTunes really works, leaving them frustrated.

Applications with complex features always require a learning curve. But it’s important to think about these goals and allow them to shape the design of every Cocoa application, even if the result isn’t perfect or ideal.

It’s easier to approach these aims when creating simple applications, so Cocoa’s design philosophy is particularly important on the iPhone and iPad. These devices are optimized for stripped-down and streamlined applications with simple, beautiful, clear interfaces. The mainstream Cocoa environment is likely to trend in this direction in the future, so it’s useful to consider mobile aesthetics when designing desktop applications.

## Understanding Aqua

Cocoa is part of Aqua. Aqua implements the visual styling of Cocoa applications, including the glassy buttons and gray window borders. Aqua also defines some specific expectations and requirements, as shown in the list that follows.

> **TIP**
> 
> You can find the guidelines online by searching for “Apple Human Interface Guidelines.” The URL occasionally changes, so it’s better to run a search than look for a specific URL.

- **Applications use multiple windows.** Windows typically float over the desktop and not inside a separate application window. There is a single menu bar at the top of the screen. Different windows do not have different menus.
- **Applications should start and quit quickly.**
- **Applications must support the OS X Dock.** Full-screen modes are allowed, and users are responsible for arranging windows on top of the Dock.
- **OS X supports multiple users.** Users should be able to use the same application on the same machine in different sessions without conflicts. OS X supports fast user switching, so users should be able to log out and log in again without losing data or settings.
- **Applications should support internationalization.** Cocoa includes features that simplify multi-language and multi-alphabet support.
- **OS X includes standard features such as preset keyboard shortcuts, color pickers, mouse actions, menu options, drag-and-drop options, and file selectors.** Cocoa applications should use these features.
- **Windows are designed with standard elements.** These elements include a data source at the left, a toolbar at the top, scroll bars at the right, further options at the bottom, and so on. Applications should follow the same outline design.

> **NOTE**
> 
> If you’re new to Cocoa, coming from a different development environment, review the design guidelines for Aqua windows. Elements such as Bottom Bars may be unfamiliar. Not all applications use all elements, but you should be aware of the different options.

- **The spacing of elements within windows is also standardized.** Standards for margins, positioning, grouping, and justification are listed in the Apple Human Interface Guidelines. For example, preferences panes, such as Safari’s preferences shown in Figure 2.1, are weighted so that they appear centered in the window, but aren’t simply center-justified in a mechanical way.
- **Fonts are partly standardized.** Most applications use the system font, but you can allow users to select other fonts in certain circumstances.
- **Applications should include help files,** with topic browsing and open searches.

**Figure 2.1**

Safari’s preferences are center-weighted rather than center-justified. The layout as a whole appears balanced, even though none of the individual items is placed on the exact vertical center line. Items are also grouped vertically for clarity.

![](img/2b293e29fc15b0797f113b85dd429b6e_42_0.png)

## Using Aqua with Cocoa

Many applications fail to follow all these design guidelines. Because OS X applications can be created and sold by any developer without Apple’s permission, developers can create their own interface standards.
