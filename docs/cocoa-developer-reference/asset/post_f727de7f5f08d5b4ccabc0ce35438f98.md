
## Introducing the Cocoa and OS X Documentation

After the brief tour of frameworks and layers earlier in the previous chapter, the OS X and Cocoa documentation should be easier to understand than if you’d dived into it cold. Apple makes the Cocoa documentation, shown in Figure 3.1, available in two places. Developers can download and install the free Xcode SDK, as described in Chapter 4. In addition to a suite of design tools, the SDK includes a full set of documentation visible in a simple Safari-based viewer. Nondevelopers and prospective developers can view the Cocoa documentation online. Currently the URL is http://developer.apple.com/mac/library/navigation.

### CAUTION

Apple occasionally rearranges its developer Web site, so the documentation URL isn’t guaranteed to remain accurate. If the URL changes, expect a redirect to the new location. If no redirect is available, you can find the location by searching for “Mac OS X Reference Library.” The library has always been freely available online and this is unlikely to change in the future. But Apple is moving away from disk-based documentation to online access, so it may not be bundled in full with future versions of Xcode.

Using the Apple documentation efficiently is a key skill, which isn’t easy to master. The documentation itself is a slightly chaotic mix of history and new features, with varying degrees of detail. The browser can also be difficult to use.

### TIP

You can solve the browser problem by using a free third-party helper application called AppKiDo, available from http://homepage.mac.com/aglee/downloads/appkido.html and shown in Figure 3.2. AppKiDo is highly recommended. It transforms and simplifies the browsing experience, and can literally save you hours of browsing time. It also groups and sorts related Cocoa classes in useful ways, making it easier to follow how Cocoa is organized.

### In This Chapter

- Understanding resource types
- Using the documentation

Figure 3.1

The developer documentation is formally known as the Mac OS X Reference Library. There’s also a separate iPhone OS Reference Library for iPhone developers.

![](img/2b293e29fc15b0797f113b85dd429b6e_79_0.png)

**Figure 3.2**

AppKiDo reads the documentation content and presents it in a more accessible form, with faster and more efficient class reference browsing. Unfortunately it only includes the Cocoa layer, not the C function layers.

![](img/2b293e29fc15b0797f113b85dd429b6e_80_0.png)

### Getting Started with the Documentation

The most important window is at the top right. In Xcode 3.2 it shows four different panes: Overview, Getting Started, Required Reading, and Featured, illustrated in Figure 3.3. The arrangement of the windows and features changes between updates, but you’ll usually find elements that are recognizably similar.

Figure 3.3

Required Reading is the best place to begin — specifically with the Cocoa Fundamentals and the introductions to Xcode and Interface Builder.

![](img/2b293e29fc15b0797f113b85dd429b6e_81_0.png)

Although Getting Started is visible by default, the Required Reading section is a better place to start. The guides to Xcode and Interface Builder are essential reading, and the Cocoa Fundamentals Guide is a good overview, although some elements are pitched at a high level of abstraction and may be difficult to follow at a first reading. The Objective-C 2.0 reference is comprehensive but terse, and is best used as a reference rather than as an introductory guide.

The Apple Human Interface Guidelines are a mix of theory and practice. The most useful section is Part III: The Aqua Interface. This has very detailed information about interface elements, including mouse cursors, function keys, key shortcut selections, and visual design standards. You should skim this section immediately and refer to it again when you begin designing an application. You’ll also find it helpful to review the interfaces of selected Apple and third-party applications. Not all of the guidelines are obvious. Even if you’re an experienced Mac user, you’ll find design suggestions and elements that you may not have consciously noticed before.

The Featured section typically includes two or three selected new articles, often about recent OS updates. The content is aimed at experienced developers and may mention a framework in any layer. It’s best to ignore these articles when starting out; they may become more useful when you’ve gained more experience.

![](img/2b293e29fc15b0797f113b85dd429b6e_82_0.png)

### TIP

The iPhone documentation follows a similar format. There’s less of it, because Cocoa Touch is smaller and simpler than Cocoa. But the outline design of both platforms is similar, and you can follow the same strategies to use the documentation efficiently.

### Understanding resource types

The rest of the documentation is divided into broad resource types. Although you’ll spend most of your time looking at the framework reference pages, it’s worth taking a few moments to explore the other resources so you can begin to familiarize yourself with the useful resources, while also noting the less useful ones.

### Articles

Articles hold a grab bag of miscellaneous essays and features, such as the Binding Your Preferences in Cocoa introduction shown in Figure 3.4. Many articles are highly specialized and of little practical interest unless you’re looking for information about a very tightly focused topic; in short, you can ignore them. For newcomers to Cocoa, the most useful articles are as follows:

- Binding Your Preferences in Cocoa
- Getting Control with Subversion and Xcode
- Installing your Application on Mac OS X: Guidelines for Developers
- Maximizing Mac OS X Application Performance
- Optimizing with Shark 4 — a series of three articles

Figure 3.5

The Getting Started with Audio & Video guide is typical of the other Getting Started articles. It's a list of links and examples padded with a short introduction, and not a true overview or orientation.

![](img/2b293e29fc15b0797f113b85dd429b6e_84_0.png)

### Guides

Guides include information about the coding interfaces to various OS X features. A small number of user interface and style guidelines also appears in this section. Guides vary in quality. Some are detailed and include source-code snippets that you can copy and paste into your applications. Others are very bare single-paragraph outlines of complex features. Only a small number are immediately useful when you're starting out. The rest detail the APIs of extremely specialized features that are rarely used.

Essential guides include the String Programming Guide, the Error Handling Programming Guide and the Undo Manager Architecture Guide, shown in Figure 3.6. You don't need to assimilate the contents of these guides immediately, but you should be aware that they exist so that you can use them as reference material when you're working with a specific Cocoa feature.

Figure 3.6

Guides typically follow a similar format — a short introduction, followed by a selection of mini-articles with more detail. Sometimes the mini-articles include sample code that you can copy and paste into your application.

![](img/2b293e29fc15b0797f113b85dd429b6e_85_0.png)

### Reference

The Reference section takes up the bulk of the documentation. Once you’ve assimilated the introductory guides, you’ll spend most of your time looking at these reference listings. There are two types of reference articles. A handful provide general reference material about broad topics, such as detailed compiler settings. Most are code references, with formal lists of properties/variables and code interfaces. This group includes Objective-C object references, and C function and struct references for all layers of OS X. Code references are grouped into the layers introduced earlier. The class references follow a fixed format, part of which is shown in Figure 3.7. A small number of class references include an extra Class at a Glance overview summary. The Table of Contents can include all or some of the following sections:

- The Overview is a short text article that sketches the function of the class and how it should be used.
- The Tasks section provides a plain list of methods grouped by function. Each method is a link — you can click it to display more information.
