

Congratulations! By reading this book, you’re taking the first step toward learning how to write less code. In three sections, you’ll learn how to use Kotlin Multiplatform (KMP) to set up and write iOS, Android and desktop apps using the latest user interface (UI) technologies.

In this book, you’ll develop several different apps — a time zone meeting helper, an app to track your list of things to do and an app that displays a list of all raywenderlich.com’s books, articles and videos.

You’ll learn how to leverage KMP by sharing business logic across platforms and creating customized native UIs in each platform. And, you’ll learn how to write tests for all your business logic, use the popular JetBrains library Ktor to handle network calls and, of course, use Kotlin Coroutines to handle concurrency.

This book requires some knowledge in mobile development but will walk you through the setup for both iOS and Android, as well as for desktop apps. While most of the book uses Kotlin, iOS developers familiar with Swift will be able to pick up Kotlin easily.

In this chapter, you’ll learn about Kotlin Multiplatform and the history of cross‑platform frameworks. At the end of the chapter, you’ll set up your environment, create a new project and run your project on Android and iOS.

Kotlin is a modern and type‑safe programming language. It incorporates null safety, preventing many of the dreaded null pointer exceptions that have plagued programming for years. Kotlin also has many innovative features — like data classes and sealed classes, extension functions that let you extend classes with functions outside of the class, lazy loading of variables and many more.

As the name implies, Kotlin Multiplatform uses the Kotlin programming language and works on multiple platforms. Kotlin already works on platforms that support the Java Virtual Machine (JVM), and it uses Kotlin Native for platforms that don’t support the JVM. Kotlin Native compiles Kotlin to native bytecode that runs natively on Apple’s operating systems, Windows and Linux. On the web, KMP compiles Kotlin to JavaScript and HTML.

KMP supports the following platforms:

- Android
- iOS
- macOS
- watchOS
- tvOS
- Windows
- Linux
- Web

That’s a lot of platforms. Some, like the web, are not stable at the moment.

# KMP vs. KMM

You use KMP to write code using Kotlin for multiple platforms. Kotlin Multiplatform Mobile (KMM) is a way to use Kotlin specifically for cross‑platform mobile development. When you’re talking about developing just for mobile devices, you’re talking about KMM — but if you’re talking about all platforms, including desktop or the web, you’re talking about KMP.

# History of cross‑platform

For as long as there have been both iOS and Android devices, developers have considered the holy grail of app development to be one codebase that could run on both. Many frameworks have tried to achieve multiplatform development, including:

- **PhoneGap**: One of the earliest, PhoneGap enabled you to write mobile apps using HTML5, CSS3 and JavaScript. It was discontinued in 2020.
- **Apache Cordova**: Open source fork of PhoneGap.
- **Ionic**: Uses Angular, React and Vue UI frameworks.
- **Appcelerator Titanium**: JavaScript‑based SDK that supported iOS, Android, Windows and Blackberry. Discontinued and will be open‑sourced by March 2022.

The frameworks above worked by using web technologies to display either native controls or controls designed to look native. However, they suffered from slow JavaScript‑to‑native communication and had to be updated every time the native platform changed.

- **Xamarin**: Microsoft‑owned C#‑based development framework that includes the .NET runtime. The framework is compiled for iOS — so it’s faster on iOS than Android, which uses a just‑in‑time compilation.
- **React Native**: Facebook’s mobile‑based framework based on the popular React web framework. It’s web‑ and JavaScript‑based. It too has a slow bridge between native and web.
- **Flutter**: This is the new kid on the block, and it works on all platforms. One of the main benefits of this framework is that you can write almost all your UI once. Some UI will need to be different based on the platform. For example, desktop and web don’t need a toolbar. One of the disadvantages is that it’s written using the Dart language, which many developers don’t know. Dart has only recently gotten null safety, and a lot of packages use code generation, which has to be done manually.

A lot of the web‑based frameworks are falling out of favor. Flutter is going strong, but many question the use of Dart.

# History of Kotlin

Kotlin has been around officially since July 2011. JetBrains released version 1.0 on February 15, 2016, and it was announced at Google I/O 2017 as a first‑class language for Android development. JetBrains developed Kotlin because most languages didn’t have the features they were looking for. JetBrains now uses Kotlin as its preferred development language for all current work — slowly replacing Java.

# Why Kotlin?

Why should you use Kotlin? Because it’s one of the only languages that you can compile for both JVM and native and use on iOS as well as the desktop and web.

Kotlin is ideal for server work as well. With the Ktor library, networking is an easy task. Writing common business logic ensures that all platforms behave the same way and you only need to test once. It uses the same code for all platforms, reducing the possibility of errors and speeding up development. Each team can use as much shared code as they want. Start slowly with existing projects, or start writing all your business logic with new projects.

iOS developers are familiar with Swift, and Kotlin is very similar — so the learning curve should be minimal. Developers still use Swift on the UI side, but they can also work and help out with business logic in Kotlin. Since there will still be a lot of iOS development work needed, iOS developers will be included in all parts of development.

# How much code to share is up to the team. If you have an existing app, you can slowly move over your business logic so you have a shared set of code that you can test once.

KMP adds minimal extra size to an app. The standard library is small and you only need to include the parts you use.

**KMM**: KMM, while newer, has become very popular. Lots of apps in the app stores already use it. Many companies find that writing their business logic once — instead of on both iOS and Android — saves the team a lot of time. The UIs are native, making the mobile developers happy, and the users are happy they have a fast experience.

# ## What KMP is not

While KMP provides Kotlin as the programming language, it doesn’t provide a UI. If you want to create a UI for Android, you can write it in native code or use the newer Jetpack Compose UI framework. For iOS, you can use UIKit or the newer SwiftUI framework using Swift. For the desktop, you can use Desktop Compose or Java Swing. In other words, you have a choice for how you write your UI. Many see this as an advantage — the UI will always be native, so it won’t suffer from the slow bridge communication that web‑based frameworks have.

# ## When to use KMP

One of the nice features of KMP and KMM is that you can use as much or as little as you want. If you have an existing app, you can use it for new features or start replacing a feature with KMP. If you start by using KMP for some of the lower layers of your app, you can reuse it for all your platforms. For instance, you can use SQLDelight to replace all your database code with just one set of code. Or, you can write your business logic just once and reuse it on all your platforms. If you need to create code to access networked APIs, you can write it once to work on all platforms.

# ## Layers

Most apps consist of different layers. There’s typically a network layer, a database layer (if needed), a repository layer that interacts with the database, a business logic layer (not always) and a UI layer. KMP doesn’t provide a UI layer; you’ll use the native UI instead.

# ### Business Logic

Most companies now have teams of iOS and Android developers. Each team

