
## WHO THIS BOOK IS FOR

This book is for the beginning iPhone developer who wants to start developing iPhone applications using the Apple iPhone SDK. To truly benefit from this book, you should have some background in programming and at least be familiar with object-oriented programming concepts. If you are totally new to the Objective-C language, you might want to jump straight to Appendix D, which provides an overview of the language. Alternatively, you can use Appendix D as a quick reference while you tackle the various chapters, checking out the syntax as you try the exercises. Depending on your learning pattern, one of those approaches may work best for you.

## WHAT THIS BOOK COVERS

This book covers the fundamentals of iPhone programming using the iPhone SDK. It is divided into 17 chapters and five appendices.

- Chapter 1: Getting Started with iPhone Programming covers the various tools found in the iPhone SDK and explains their uses in iPhone development.
- Chapter 2: Write Your First Hello World! Application gets you started with Xcode and Interface Builder to build a Hello World application. The focus is on getting your hands dirty, and more details on the various parts and components are covered in subsequent chapters.
- Chapter 3: Outlets, Actions, and View Controllers covers the fundamental concepts of iPhone programming; outlets and actions. You learn how outlets and actions allow your code to interact with the visual elements in Interface Builder and why they are an integral part of every iPhone application.
- Chapter 4: Exploring the Views describes the use of the various views that make up the user interface (UI) of your iPhone applications. You learn the techniques to manipulate the UI of your application, as well as how views are stored internally.
- Chapter 5: Keyboard Inputs shows you how to deal with the virtual keyboard in your iPhone. You see how to hide the keyboard on demand and how to ensure that your views are not blocked by the keyboard when it is displayed.
- Chapter 6: Screen Rotations demonstrates how you can reorient your application's UI when the device is rotated. You learn about the various events that are fired when the device is rotated. You also learn how to force your application to display in a certain orientation.
- Chapter 7: View Controllers shows how you can create an application with multiple views. You learn how to build an iPhone application using the Window-based Application template.
- Chapter 8: Tab Bar and Navigation Applications shows you how to build Tab Bar applications and Navigation applications using the templates provided by the SDK. Using these two application templates, you can create sophisticated multiview applications.
- Chapter 9: Utility Applications shows you how to build yet another type of application in the iPhone — utility applications.

## HOW THIS BOOK IS STRUCTURED

This book breaks down the task of learning iPhone programming into several smaller chunks, allowing you to digest each topic before delving into another more advanced topic. In addition, there are a few chapters that cover topics already discussed in the previous chapter. This is because there is usually more than one way of doing things in Xcode and Interface Builder, and hence this approach allows you to learn the different techniques in developing iPhone applications.

If you are a total beginner to iPhone programming, it would be motivational for you to start with Chapters 1 and 2. Once you have gotten things moving, head on to the Appendices to read more about the tools and language you are using. Once you are ready, you can now continue with Chapter 3 and gradually move into more advanced topics.

A feature of this book is that all the code samples in each chapter are independent of those discussed in previous chapters. That way, you have the flexibility to dive into the topics that interest you and start working on the Try It Out labs.

## WHAT YOU NEED TO USE THIS BOOK

Most of the examples in this book run on the iPhone Simulator (which comes as part of the iPhone SDK). For exercises that access the hardware (such as the camera and accelerometer), you need a real iPhone or iPod Touch. Appendix E shows how you can test your application on a real device. For applications that access the phone function, you need an actual iPhone (the iPod Touch has no built-in phone).

In general, to get the most out of this book, having a real iPhone or iPod Touch is not necessary (although it is definitely required for testing if you plan to deploy your application on the App Store).

## CONVENTIONS

To help you get the most from the text and keep track of what's happening, we've used a number of conventions throughout the book.

### TRY IT OUT — These Are Exercises or Examples for You to Follow

The Try It Out exercises appear once or more per chapter as exercises to work through as you follow the text in the book.

1. They usually consist of a set of numbered steps.
2. Follow the steps through with your copy of project files.

### How It Works

After each Try It Out, the code you've typed is explained in detail.

> **WARNING** Boxes like this one hold important, not-to-be-forgotten information that is directly relevant to the surrounding text.

> **NOTE** Notes, tips, hints, tricks, and asides to the current discussion look like this.

As for other conventions in the text:

- New terms and important words are *highlighted* in italics when first introduced.
- Keyboard combinations are treated like this: Control-R.
- Filenames, URLs, and code within the text are treated like so: `persistence.properties`.
- Code is presented in two different ways:

```
We use a monofont type with no highlighting for most code examples.
We use bolding to emphasize code that is of particular importance in the present context.
```

## SOURCE CODE

As you work through the examples in this book, you may choose either to type in all the code manually or to use the source code files that accompany the book. All the source code used in this book is available for download at www.wrox.com. When at the site, simply locate the book's title (use the Search box or one of the title lists) and click the Download Code link on the book's detail page to obtain all the source code for the book. Code that is included on the Web site is highlighted by the following icon.

![](img/aab2d775c46f70cd606f2e58e2521324_26_0.png)

Listings include the filename in the title. If it is just a code snippet, you'll find the filename in a code note such as this.

> **NOTE** Because many books have similar titles, you may find it easiest to search by ISBN: this book's ISBN is 978-0-470-50097-2

After you download the code, just decompress it with your favorite compression tool. Alternatively, go to the main Wrox code download page at www.wrox.com/dynamic/books/download.aspx to see the code available for this book and all other Wrox books.

## ERRATA

We make every effort to ensure that there are no errors in the text or in the code. However, no one is perfect, and mistakes do occur. If you find an error in one of our books, such as a spelling mistake or faulty piece of code, we would be very grateful for your feedback. By sending in errata, you may save another reader hours of frustration and at the same time help us provide even higher-quality information.

To find the errata page for this book, go to www.wrox.com and locate the title using the Search box or one of the title lists. Then, on the book details page, click the Book Errata link. On this page, you can view all errata that has been submitted for this book and posted by Wrox editors. A complete book list including links to each book's errata is also available at www.wrox.com/misc-pages/booklist.shtml.

If you don't spot "your" error on the Book Errata page, go to www.wrox.com/contact/techsupport.shtml and complete the form there to send us the error you have found. We'll check the information and, if appropriate, post a message to the book's errata page and fix the problem in subsequent editions of the book.

## P2P.WROX.COM

For author and peer discussion, join the P2P forums at p2p.wrox.com. The forums are a Web-based system for you to post messages relating to PHP books and related technologies and interact with other readers and technology users. The forums offer a subscription feature to e-mail you topics of interest of your choosing when new posts are made to the forums. Wrox authors, editors, other industry experts, and your fellow readers are present on these forums.

At http://p2p.wrox.com, you will find a number of different forums that will help you not only as you read this book but also as you develop your own applications. To join the forums, just follow these steps:

1. Go to p2p.wrox.com and click the Register link.
2. Read the terms of use and click Agree.
3. Complete the required information to join as well as any optional information you want to provide and click Submit.
4. You will receive an e-mail with information describing how to verify your account and complete the joining process.

> **NOTE** You can read messages in the forums without joining P2P, but to post your own messages, you must join.
