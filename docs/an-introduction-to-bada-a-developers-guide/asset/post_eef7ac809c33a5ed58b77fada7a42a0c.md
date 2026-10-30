
of processes. Experience has shown that so-called agile software development processes are very appropriate for fast-paced software, which mobile apps definitely are.

In the agile manifesto³ software engineering experts have summarised the key factors that should help to produce better software faster and more reliably. They state that agile development is about *focus on result*. This means executable software should be built as soon as possible, which is the primary measure of progress. Software should be built *incrementally* starting from its core functions over various *iterations*. Tool and process support is relevant but must be *appropriate* to the solution in order to avoid unnecessary overhead. Finally software engineering is about people working together. Hence, *communication* – ideally in a face-to-face and spoken way – is at the core of agile development. This not only refers to the project team but also, and just as importantly, to the stakeholders, clients, and future end-users.

In line with this, we would like to add to this recommendation an emphasis on using as much *prototyping* and *diverse testing* as possible throughout the whole development, where both are integral parts of and inherently supported by the bada platform and its development tools. Prototypes can be exploited in nearly any phase during the development of mobile software solutions. They are primarily helpful for eliciting requirements or to get a common understanding with various stakeholders early in the project. Testing certainly is not unique to mobile software engineering but must be treated and executed differently in mobile development. This is an effect of various issues related to mobile software such as the heterogeneity of hardware and devices, the dependence on context factors that are difficult to test on simulators (e.g. geographic locations), and the phenomenon of the discrepancy between simulator and real device behaviour.

The bada toolkit provides means to support both. First, the UI Builder, which is integrated into the bada IDE, allows building simple mock-up prototypes easily and quickly. Developers can use this WYSIWYG tool to create first ‘clickable’ demos by visually placing a variety of UI controls on the device screen. A second convenient tool is the Event Injector that comes with the bada Simulator. This is useful for simulating a broad variety of context data. Incoming calls, text messages, and battery level can be tested, as well as location and sensors, including acceleration, tilt, compass, and proximity. It is always difficult to test mobile apps in a simulator because obviously you are missing all the context data, which is so necessary. By far the more expensive and complex type of test is deployment on real devices and test-runs in the real-world context. With the bada Event Injector (see Figure 1.2), a lot of this effort can be shifted to Simulator tests, making system tests less time consuming and cheaper.

![](img/a257d5fd53a79a244a20e587cd2f08f6_39_0.png)

Figure 1.2 The bada Event Injector.

But let us return to the ideas postulated by the agile manifesto. Often, ‘agile’ is misused to describe everything that does not have clear rules or a process. We would rather call this ‘cowboy coding’. Agile cannot be equated to chaos, or lack of rules or discipline. Agile app development does propose following some simple maxims and recommendations.

So, let us describe some rules. We do so by listing a toolbox of some best-practices coming from various agile methodologies such as Scrum, Test-driven Development, eXtreme Programming, and Crystal. Again, the core cornerstones are focus on results, incremental iterations, appropriateness of the means, and communication. The following best-practice recommendations all deal with one or more of these cornerstones:

- Focus on results more than on processes. Every procedure or means that does not help to achieve the goal of the software project should be cut off. The more complex a project, the more tools, rules, and formalisms it will require.
- Plan your software development into cycles or iterations. Identify the core and most critical components and priorities, and start with the most important ones (‘first things first’).
- Be tolerant towards change (changing requirements and change requests). Avoid rigid or inflexible structures, processes, tools, or methods.
- Try to produce executable software at the end of every iteration.
- Treat each iteration as an increment to the final software product.
- Try to keep design and software simple. Have possible extensions in mind but focus on producing executable code at least at the end of each iteration (‘keep it short and simple – KISS’).
- Make use of early feedback from various stakeholders, such as your client or end-users. User acceptance tests could possibly be integrated into every iteration.
- In the early stages, even use paper and pen to sketch software designs or early prototypes.
- Make use of a test-oriented development where you write the test cases first, at least for core or critical code parts.
- Build and integrate tested parts frequently (e.g. daily).
- Set up communication channels such that close contact with client and end-users is possible.
- Try to have regular, frequent, and brief intra-team communication without a formal overhead (e.g. daily stand-up meetings).
- Establish and publish team and project rules – such as a communication etiquette or coding standards.
- Conduct code reviews or pair programming sessions for core or critical code parts.
- Make sure you have efficient knowledge transfer within the team but also to client and user. This may not always be applicable or sensible. Sometimes this knowledge transfer may also be unidirectional.
- Use visualisation for your communication. Use, for instance, a visible whiteboard accessible to everyone in the team for sketching the tasks or features, and development progress.
- Although some form of documentation is necessary, keep it to a minimum: only as much as is necessary. And beware of over-specification.

Again, please bear in mind that you do not have to stick to the mobile software engineering best-practices outlined here. This is simply advice and something you can stick to.

## CHAPTER 2 bada Basics

This chapter gets straight down to the essentials of developing native bada applications in C++. We’ll see just how easy it is to get a first skeleton application up and running on the bada Simulator.

To start with, this little app doesn’t do much – think *Hello World*! But this is the code at the heart of every bada app, and as we’ll see in the next few chapters, bada makes it easy to build up from this basic skeleton to create a full-featured, native application.

> **Note:** At the time of writing the SDK version is 1.0.0 beta3. Current SDKs install on Microsoft Windows only. It’s likely that bada will support other development options eventually, but nothing is currently announced. The Simulator launches from the Eclipse-based bada IDE, which is included in the SDK.

### What You Will Learn

This chapter aims to get you started quickly. You will learn:

- How to create a simple application using the Application Wizard.
- How to add a simple UI using UI Builder.
- How to use the developer and publishing services provided by the bada developer portal.
- How to build for and deploy to a phone.

### What You Will Need

This book assumes beginner’s C++ skills. If you don’t know C++, don’t give up: bada works hard to make the app developer’s life as easy as possible. If you have experience using any modern programming language, a good C++ primer should be enough to get you up and running.

By the way, don’t worry if you are new to mobile development. As we saw in the previous chapter, there are some things that make mobile unique, and different from the world of the desktop. We’ll highlight those issues as they arise in the context of each chapter.

### 2.1 Your First bada Application

Native bada apps are C++ executables that combine the code that you write with framework code. Because the bada framework takes care of the basic functionality that every app requires, there is very little code required to create a minimal app, as we will see.

To start with, we will build for the bada Simulator only. Later in the chapter we’ll dig a little deeper and show you how to build for (and deploy to) a real bada phone.

Because bada is highly modular, most of your time as a developer will be spent connecting together the pieces while the bada frameworks do the heavy lifting for you.

As you might expect, all bada applications are fully graphical programs. In fact, one easy way to think of a bada application is as a GUI that does something.

For any app, the GUI is where the user and the app meet. It’s the GUI that presents the application functionality to the user, and the GUI that allows the user to control that functionality. In fact for the user, your GUI is your app, and to a large degree determines the complete app experience.

All bada apps that use the standard UI elements share the distinctive look-and-feel and behaviour of the bada UI and application frameworks. When you need more customised elements, you can derive your own and extend the default behaviour. Of course, there may be times when you want complete UI control (in a game, for example), and don’t want the standard look and feel. In that case bada allows you to write directly to the full-screen display to construct your own UI from scratch.
