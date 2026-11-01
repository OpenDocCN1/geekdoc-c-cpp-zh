
## HOW THIS BOOK IS STRUCTURED

This book breaks down the task of learning iPhone programming into several smaller chunks, allowing you to digest each topic before delving into another more advanced topic. In addition, there are a few chapters that cover topics already discussed in the previous chapter. This is because there is usually more than one way of doing things in Xcode and Interface Builder, and hence this approach allows you to learn the different techniques in developing iPhone applications.

If you are a total beginner to iPhone programming, it would be motivational for you to start with Chapters 1 and 2. Once you have gotten things moving, head on to the Appendices to read more about the tools and language you are using. Once you are ready, you can now continue with Chapter 3 and gradually move into more advanced topics.

A feature of this book is that all the code samples in each chapter are independent of those discussed in previous chapters. That way, you have the flexibility to dive into the topics that interest you and start working on the Try It Out labs.

## WHAT YOU NEED TO USE THIS BOOK

Most of the examples in this book run on the iPhone Simulator (which comes as part of the iPhone SDK). For exercises that access the hardware (such as the camera and accelerometer), you need a real iPhone or iPod Touch. Appendix E shows how you can test your application on a real device. For applications that access the phone function, you need an actual iPhone (the iPod Touch has no built-in phone).

In general, to get the most out of this book, having a real iPhone or iPod Touch is not necessary (although it is definitely required for testing if you plan to deploy your application on the AppStore).

## CONVENTIONS

To help you get the most from the text and keep track of what's happening, we've used a number of conventions throughout the book.

## TRY IT OUT These Are Exercises or Examples For You to Follow

The Try It Out exercises appear once or more per chapter as exercises to work through as you follow the text in the book.

- 1. They usually consist of a set of numbered steps.
- 2. Follow the steps through with your copy of project files.

## How It Works

After each Try It Out, the code you've typed is explained in detail.

## ERRATA

We make every effort to ensure that there are no errors in the text or in the code. However, no one is perfect, and mistakes do occur. If you find an error in one of our books, such as a spelling mistake or faulty piece of code, we would be very grateful for your feedback. By sending in errata, you may save another reader hours of frustration and at the same time help us provide even higher-quality information.

To find the errata page for this book, go to www.wrox.com and locate the title using the Search box or one of the title lists. Then, on the book details page, click the Book Errata link. On this page, you can view all errata that has been submitted for this book and posted by Wrox editors. A complete book list including links to each book's errata is also available at www.wrox.com/misc-pages/booklist.shtml.

If you don't spot "your" error on the Book Errata page, go to www.wrox.com/contact/techsupport.shtml and complete the form there to send us the error you have found. We'll check the information and, if appropriate, post a message to the book's errata page and fix the problem in subsequent editions of the book.

## P2P.WROX.COM

For author and peer discussion, join the P2P forums at p2p.wrox.com. The forums are a Web-based system for you to post messages relating to Wrox books and related technologies and interact with other readers and technology users. The forums offer a subscription feature to e-mail you topics of interest of your choosing when new posts are made to the forums. Wrox authors, editors, other industry experts, and your fellow readers are present on these forums.

At http://p2p.wrox.com, you will find a number of different forums that will help you not only as you read this book but also as you develop your own applications. To join the forums, just follow these steps:

- 1. Go to p2p.wrox.com and click the Register link.
- 2. Read the terms of use and click Agree.
- 3. Complete the required information to join as well as any optional information you want to provide and click Submit.
- 4. You will receive an e-mail with information describing how to verify your account and complete the joining process.

> **NOTE** You can read messages in the forums without joining P2P, but to post your own messages, you must join.

## 系统设置

自定义 iOS 设备的数据类型与采集方式

为满足不同业务场景的数据需求，您可以根据实际需要，自由添加、编辑或删除数据类型。灵活配置采集方式，让数据采集更好地服务于您的业务目标。

## 已添加类型

共3项

| 数据类型 | 采集方式 | 启用状态 | 操作 |
| --- | --- | --- | --- |
| 应用使用情况 | 系统自动采集 | 已开启 | 编辑 删除 |
| 设备信息 | 系统自动采集 | 已开启 | 编辑 删除 |
| 网络流量 | 系统自动采集 | 已开启 | 编辑 删除 |

添加数据类型

选择数据类型

```
```
▼ 应用使用情况
```
```

设置采集方式

○ 系统自动采集  ○ 用户手动填写

启用该数据类型

启用后，系统将按照设定的方式采集该类型的数据。

取消

确认添加

## 1

## Getting Started with
 iPhone Programming

## WHAT YOU WILL LEARN IN THIS CHAPTER

- How to obtain the iPhone SDK
- The components included in the iPhone SDK
- The Features of the development tools — Xcode, Interface Builder, iPhone Simulator
- The Capabilities of the iPhone Simulator
- The Architecture of the iPhone OS
- The Frameworks of the iPhone SDK
- The Limitations and characteristics of the iPhone

Welcome to the world of iPhone programming! That you are now holding this book shows that you are fascinated with the idea of developing your iPhone applications and want to join the ranks of those tens of thousands of developers whose applications are already deployed in the AppStore.

As the old Chinese adage says, “To accomplish your mission, first sharpen your tools.” Successful programming requires you first of all to know your tools well. Indeed, this couldn’t be more true for iPhone programming — you need to know quite a few tools before you can even get started. Hence, the goal of this chapter is to show you the various relevant tools and information you need to jump on the iPhone development bandwagon.

Without further ado, it’s time to get down to work.

## OBTAINING THE IPHONE SDK

To develop for the iPhone or iPod Touch, you first need to sign up as a Registered iPhone Developer at http://developer.apple.com/iphone/program/start/register/. The registration is free and provides you with access to the iPhone SDK and other resources that are useful for getting started.

After signing up, you can download the iPhone SDK (see Figure 1-1).

![](img/16991b58db5894715c4a443315e06a22_33_0.png)

FIGURE 1-1

Before you install the iPhone SDK, make sure you satisfy the following system requirements:

- Only Intel Macs are supported, so if you have another processor type (such as the older G4 or G5 Macs), you're out of luck.
- You have updated your system with the latest Mac OS X release.

An iPhone/iPod Touch device is highly recommended, though not strictly necessary. To test your application, you can use the included iPhone Simulator. However, if you want to test certain hardware features like the camera, accelerometer, and such, you would need to use a real device.

When the SDK is downloaded, proceed with installing it (see Figure 1-2). You will be asked to accept a few licensing agreements and then select the destination folder in which to install the SDK.

![](img/16991b58db5894715c4a443315e06a22_34_0.png)

FIGURE 1-2

If you have selected the default settings during the installation phase, after the installation you should be able to find the various tools installed in the `/Developer/Applications` folder (see Figure 1-3).

![](img/16991b58db5894715c4a443315e06a22_34_1.png)

FIGURE 1-3

## COMPONENTS OF THE IPHONE SDK

The iPhone SDK includes a suite of development tools to help you develop applications for your iPhone and iPod Touch. It includes:

- Xcode — the Integrated Development Environment (IDE) that allows you to manage, edit, and debug your projects.
- Dashcode — the Integrated Development Environment (IDE) that allows you to develop web-based iPhone applications and Dashboard Widgets. Dashcode is beyond the scope of this book.
