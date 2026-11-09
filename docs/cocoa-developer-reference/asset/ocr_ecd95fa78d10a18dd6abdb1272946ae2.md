![](bbox=[0.103, 0.128, 0.171, 0.183])

# TIP

It’s easy for new developers to feel overwhelmed by the number of frameworks and objects. No one with a normal human IQ can remember the entire OS X documentation set. A more practical learning strategy is to master an outline of the relationships between the most useful frameworks in OS X, and then find the rest of their details in the documentation when necessary. You don’t need to remember *everything* — but it’s helpful to remember where to look when you need to find something.

Table 2.4 shows a simplified view of the OS X layers that strips them down to essentials. This model doesn’t match Apple’s own classification scheme, but it does match how you’re likely to work with layers in practice. In a typical application you’ll use the Cocoa Layer to build an application skeleton and to manage key application events and data, and you’ll use the Services Layer to manage media and data. Many applications ignore the OS Layer completely, or they hardly ever access it. You’ll need to work with it if you create or manage drivers or access the Mac’s hardware features. Otherwise, you can ignore most of its features.

| Framework | Interface | Applications and Elements |
|---|---|---|
| “Cocoa Layer” | Objective-C objects and methods | Window, interface, and application management; high-level media features; packaged animation effects; object-oriented data; high-level Web and network access; high-level timer and thread control. |
| “Services Layer” | C functions and data structures | Low-level media features, including basic graphic primitives and customized animations; C-type data structures; low-level Web and network access. This layer duplicates some of Cocoa’s features with an alternative C function interface. |
| “OS Layer” | C functions and data structures | Useful functions that aren’t included in the other layers, such as random number generation. Socket-level Web and network access; system and hardware access; low-level process and thread control. |

Switching between layers as you work is standard practice. You can simplify development by understanding that most Mac applications are a mix of Objective-C objects and standard C function calls, that there’s some feature duplication across the layers, and that the further you get from the user, the more you’ll be using OS X’s C libraries rather than Cocoa. Figure 2.4 shows a common workflow.