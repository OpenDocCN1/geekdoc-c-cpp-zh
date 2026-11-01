
Chapter 8: Application Preferences discusses the use of application settings to persist application preferences. Using application settings, you can access preferences related to your application through the Settings application available on the iPad.

Chapter 9: File Handling shows how you can persist your application data by saving the data to files in your application's sandbox directory. You also learn how to access the various folders available in your application sandbox.

Chapter 10: Database Storage Using SQLite3 covers the use of the embedded SQLite3 database library to store your data.

Chapter 11: Simple Animations provides an overview of the various techniques you can use to implement simple animations on the iPad. You also learn about the various affine transformations supported by the iPhone SDK.

Chapter 12: Recognizing Gestures provides an overview of the various gesture recognizers available in the iPhone SDK to help your device interpret user's input gestures.

Chapter 13: Accessing the Accelerometer shows how you can access the accelerometer that comes with every iPad. You will also learn how to detect shakes to your device.

Chapter 14: Web Services teaches you how to consume Web services from within your iPad application. You will learn the various ways to communicate with Web services — SOAP, HTTP GET, and HTTP POST. You will also learn how to parse the returning XML result returned by the Web service.

Chapter 15: Bluetooth Programming explores the use of the Game Kit framework for Bluetooth programming. You will learn how to get two iPads to communicate using a Bluetooth connection. You will also learn how to implement voice chatting over a Bluetooth connection.

Chapter 16: Bonjour Programming shows how you can publish services on the network using the Bonjour protocol.

Chapter 17: Apple Push Notification Services explains how you can implement applications that use push notifications. The APNs allows your applications to constantly receive status updates from a service provider even though the application may not be running.

Chapter 18: Displaying Maps shows how to build location-based services application using the Map Kit framework. You will also learn how to obtain geographical locations data and use them to display a map.

Appendix A: Answers to Exercises contains the solutions to the end-of-chapter exercises found in every chapter except Chapter 1.

Appendix B: Getting Around in Xcode provides a quick run-through of the many features in Xcode.

Appendix C: Getting Around in Interface Builder provides an overview of the many features of Interface Builder.

Appendix D: Crash Course in Objective-C provides a crash course in Objective-C. Readers who are new to this language should read this chapter before getting started.

## HOW THIS BOOK IS STRUCTURED

This book breaks down the task of learning iPad programming into several smaller chunks, allowing you to digest each topic before delving into a more advanced topic. In addition, there are a few chapters that cover topics already discussed in the previous chapter. That's because there is usually more than one way of doing things in Xcode and Interface Builder, and hence this approach allows you to learn the different techniques in developing iPad applications.

If you are a total beginner to iPad programming, start with Chapters 1 and 2. Once you have gotten things moving, head on to the appendixes to read more about the tools and language you are using. Once you are ready, you can now continue with Chapter 3 and gradually move into more advanced topics.

A feature of this book is that all the code samples in each chapter are independent of those discussed in previous chapters. That way, you have the flexibility to dive into the topics that interest you and start working on the Try It Out projects.

## WHAT YOU NEED TO USE THIS BOOK

Most of the examples in this book run on the iPhone Simulator (which comes as part of the iPhone SDK). For exercises that access the hardware (such as the accelerometer), you need a real iPad. In general, to get the most out of this book, having a real iPad device is not necessary (although it is definitely required for testing if you plan to deploy your application on the AppStore).

## CONVENTIONS

To help you get the most from the text and keep track of what's happening, we've used a number of conventions throughout the book.

## TRY IT OUT These Are Exercises or Examples for You to Follow

The Try It Out exercises appear once or more per chapter as exercises to work through as you follow the text in the book.

- 1. They usually consist of a set of numbered steps.
- 2. Follow the steps through with your copy of project files.

### How It Works

After each Try It Out, the code you've typed is explained in detail.

As for other conventions in the text:

- New terms and important words are highlighted in italics when first introduced.
- Keyboard combinations are treated like this: Control-R.
- Filenames, URLs, and code within the text are treated like so: `persistence.properties.`
- Code is presented in two different ways:
  - We use a monofont type with no highlighting for most code examples.
  - We use bolding to emphasize code that is of particular importance in the present context.

**WARNING** Boxes like this one hold important, not-to-be forgotten information that is directly relevant to the surrounding text.

**NOTE** Notes, tips, hints, tricks, and asides to the current discussion look like this.

**COMMON MISTAKES** This feature, Common Mistakes, helps you avoid the obstacles that many new practitioners find themselves negotiating.

## SOURCE CODE

As you work through the examples in this book, you may choose either to type in all the code manually or to use the source code files that accompany the book. All the source code used in this book is available for download at www.wrox.com. When at the site, simply locate the book's title (use the Search box or one of the title lists) and click the Download Code link on the book's detail page to obtain all the source code for the book. Code that is included on the Web site is highlighted by the following icon and/or CodeNote, as shown following the icon:

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_30_0.png)

Listings include the filename in the title. If it is just a code snippet, you’ll find the filename in a CodeNote such as this:

```
code snippet filename
```

After you download the code, just decompress it with your favorite compression tool. Alternatively, go to the main Wrox code download page at www.wrox.com/dynamic/books/download.aspx to see the code available for this book and all other Wrox books.

## ERRATA

We make every effort to ensure that there are no errors in the text or in the code. However, no one is perfect, and mistakes do occur. If you find an error in one of our books, such as a spelling mistake or faulty piece of code, we would be very grateful for your feedback. By sending in errata, you may save another reader hours of frustration and at the same time help us provide even higher-quality information.

To find the errata page for this book, go to www.wrox.com and locate the title using the Search box or one of the title lists. Then, on the book details page, click the Book Errata link. On this page, you can view all errata that has been submitted for this book and posted by Wrox editors. A complete book list including links to each book's errata is also available at www.wrox.com/misc-pages/booklist.shtml.

**NOTE** Because many books have similar titles, you may find it easiest to search by ISBN; this book's ISBN is 978-0-470-64165-1.

If you don't spot "your" error on the Book Errata page, go to www.wrox.com/contact/techsupport.shtml and complete the form there to send us the error you have found. We'll check the information and, if appropriate, post a message to the book's errata page and fix the problem in subsequent editions of the book.

## P2P.WROX.COM

For author and peer discussion, join the P2P forums at p2p.wrox.com. The forums are a Web-based system for you to post messages relating to Wrox books and related technologies and interact with other readers and technology users. The forums offer a subscription feature to e-mail you topics of interest of your choosing when new posts are made to the forums. Wrox authors, editors, other industry experts, and your fellow readers are present on these forums.

At http://p2p.wrox.com, you will find a number of different forums that will help you not only as you read this book but also as you develop your own applications. To join the forums, just follow these steps:

- 1. Go to p2p.wrox.com and click the Register link.
- 2. Read the terms of use and click Agree.
