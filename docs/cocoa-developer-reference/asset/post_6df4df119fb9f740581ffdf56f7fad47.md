
## Chapter 19: Developing for the iPhone and iPad ........................................ 493

- Introducing the iPhone, iPod touch, and iPad ........................................ 494
  - Comparing iOS and OS X applications ........................................ 495
  - Understanding the mobile app business model ........................................ 498
- Moving to iOS from OS X ........................................ 502
  - Getting started with the iPhone SDK ........................................ 502
  - Understanding iOS app design goals ........................................ 503
  - Understanding key iOS coding differences ........................................ 505
  - Considering iOS and hardware compatibility ........................................ 505
- Understanding iOS Views and UI Design ........................................ 505
  - Working with windows and views on the iPhone ........................................ 505
  - Managing orientation ........................................ 509
  - Adding navigation and control features ........................................ 511
  - Handling touch events ........................................ 514
  - Working with windows and views on the iPad ........................................ 515
- Developing for iOS in Xcode ........................................ 516
  - Using the Xcode Simulator ........................................ 516
  - Introducing the Xcode templates ........................................ 517
- Building a Simple Application ........................................ 524
  - Adding view controller subclasses ........................................ 526
  - Implementing the view controllers ........................................ 526
  - Creating views ........................................ 528
  - Handling events with protocol messaging ........................................ 532
  - Creating an animated view swap ........................................ 534
- Selling in the App Store ........................................ 536
  - Understanding certificates, provisioning profiles, and permissions ........................................ 538
  - Packaging an app for the App Store ........................................ 541
  - Uploading an app to the App Store ........................................ 542
- Summary ........................................ 543

## Part IV: Appendices ........................................ 545

## Appendix A: Building Dashboard Widgets ........................................ 547

## Appendix B: Maximizing Productivity and Avoiding Errors ........................................ 565

## Index ........................................ 575

## Preface

When I started developing for the iPhone after a fifteen-year break from software, my first thought was: *What is going on here?* I'd written machine code for Macs and had some experience with earlier versions of Mac OS. It soon became obvious that Cocoa Touch was doing clever things behind the scenes, and that my apps were supposed to be exchanging information with those clever things.

Unfortunately, neither the official documentation nor unofficial sources of help were making it clear what those things were.

With enough persistence, it's possible for almost any developer to reverse-engineer the documentation and answer the "What is going on here?" question for himself or herself. But it's more productive to have that information before starting out. So my first goal for this book is to equip you, as a developer, with the key concepts you need to build Cocoa projects efficiently and productively.

Understanding Cocoa means more than being able to name-check concepts like delegation and Model-View-Controller; it means learning how Cocoa applies these concepts, how they influence the design of Cocoa's classes, and how your code can leverage the features built into Cocoa to simplify projects and minimize development time. In short, it means discovering how to *think* Cocoa. New features will begin to feel intuitive once you understand the reasoning behind them.

My second goal for the book is to give readers the skills they need to answer Cocoa questions for themselves, without handholding. OS X is vast and complex, and a full printed guide of every feature would have to be delivered on a truck. Books always sell better when readers can pick them up and take them home without stalling traffic, so this book doesn't try to detail every Cocoa feature. It also doesn't try to build complex sample projects that are unlikely to match your specific needs. Instead, it gives you the skills you need to find answers to questions for yourself, using the official documentation and other sources of insight.

One feature you won't find in this book is cheerleading. Like any other development environment, Cocoa is a mix of excellence and unpredictability. Cocoa's best features are almost super-naturally productive and take you where you want to go with almost no code at all. Other elements offer a more scenic journey through less intuitive class relationships. Instead of a sales pitch, this book gives you a guided tour of the highlights but also warns you about some of the more dangerous parts of town.

Finally, software is as much an art as a science. Art is about creating captivating, enjoyable, and colorful experiences for an audience. In common with the Apple ethic, this book is deliberately less formal and more creative than a pure software reference. You'll find the rules here. And sometimes you'll also find suggestions for breaking the rules.

Every author tries to make his or her books as helpful as possible. Comments and feedback are welcome at cocoadr@zettaboom.com.

## Acknowledgments

Books don’t write themselves — not yet, anyway. Until operating systems become self-documenting, writing a book continues to be a team effort.

I’d like to thank acquisitions editor Aaron Black for enthusiastically suggesting the project and project editor Marty Minner for his support and for taking the manuscript and producing a book from it. Sincere thanks are also due to the rest of the team at Wiley for their hard work behind the scenes.

Software development has become a communal activity, and particular appreciation is due to the countless bloggers, experimenters, developers, and problem-solvers on the Web whose generosity and creativity have made so much possible in so many ways.

Finally — love as always for Team HGA. I couldn’t have written it without you.

## Introduction

This book is about developing Cocoa projects for OS X using the Xcode SDK. The theoretical elements of Cocoa are similar to those in Cocoa Touch and apply equally to both OS X and iOS. The more practical elements were written to describe OS X but with significant overlap with the equivalent features in iOS.

You'll find this book useful if you're a newcomer to Cocoa at the beginner or intermediate level and have experience with C/C++/C#, Java, Flash, Python, or a Web language such as PHP. If you're ambitious and feel up to a challenge, you can start with no experience at all. If you do, you'll find it helpful to use Objective-C (Wiley, 2010) as a companion title.

Cocoa isn't a synonym for OS X, and for practical reasons this book says little about the low-level Mach/POSIX features that underpin OS X. It mentions some of the C-level frameworks that Cocoa is built on but doesn't detail them, although it does give you enough information to explore them for yourself if you choose to.

Chapter 1 is an introduction to the history of Cocoa and OS X and explains how Cocoa evolved from Smalltalk and from the Objective-C development environment introduced by NeXT in the late 1980s. It also includes some strategic hints about the OS X and iOS application markets and how to research the current state of both so that you can target your applications for maximum return.

Chapter 2 is an informal introduction to the features that make Cocoa unique. Whether you're starting programming from scratch, or have a background in some other environment, this is one of the most critical chapters in the book. Reading it will save you time later.

Chapter 3 is a guide to the Apple documentation. It may not be obvious why this needs a guide, but Apple has structured the documentation in specific ways, and you'll progress more quickly and with less effort if you understand what this means in practice. Understanding and using the documentation is a key skill. Don't skip this chapter, even if you already have experience in other environments.

Chapter 4 explains how to join Apple's Developer Programs, and how to download and install Xcode. It also introduces the key features of Xcode 3.2.3, including the windows, menu items, and customizable toolbar. This chapter explains how to create a new sample project — an essential skill that's used repeatedly later in the book.

Chapter 5 introduces objects and classes and describes how they're implemented in Objective-C. If you have experience in other object-oriented environments, you'll need this chapter to reorient yourself to Objective-C. If you haven't, you'll find an explanation of object-oriented development that's a fundamental requirement for understanding Cocoa.

Chapter 6 explores objects in Cocoa in a more hands-on way, with very simple projects that illustrate how to use objects and their features in real Cocoa applications.

Chapter 7 introduces the key features of Interface Builder and explains how you can use IB to build complete applications, because IB isn't just for interfaces.
