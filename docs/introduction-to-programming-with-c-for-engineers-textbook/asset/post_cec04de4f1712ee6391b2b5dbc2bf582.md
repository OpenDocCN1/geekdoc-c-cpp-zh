
In our example, the entire suite of project files is generated. From these, _EmptyPro.sln_ should be opened in Visual C++, and the _Rebuild Solution_ command should be launched. If everything is OK, then the project should be built successfully.9 In Linux,10 after generating the project with _CMake_, the build process is activated by launching _make_. An example for the Grades project, discussed in Section 3.2, looks like this:

```
boxy@PARSEC:~/Projects/Grades/build_linux$ make
```

Unfortunately, in life, things are not always that easy. If an error happens, then we need to find the first place where it occurred. Then we need to understand the error message. Sometimes this chore is easier if we copy the message to a more convenient editor, where we can split it into more meaningful parts. If they tell us what is wrong, then we can try to figure out how to fix the problem. If errors occur when running the _CMake_ script, remember to delete all previously generated files in the `build_xxx` directory. Sometimes an update or a new installation of a compiler suite or _CMake_ is necessary. However, before taking such drastic steps, checking the Internet usually provides answers.

Let's now change the previous script a little to make it generate all necessary files for the _EasyMatrix_ projects presented in Section 3.5. In this case, we have more files in the project, as follows:

```
[+]build_linux
[+]build_mac
[+]build_win
|--CMakeLists.txt
[+]include
|--EMatrix.h
|--EMUtility.h
|--MarsXorShift.h
|--ReadMe.txt
[+]src
|--EMatrix.cpp
|--EMTest.cpp
|--EMUtility.cpp
|--main.cpp
```

The only change we need to make to the _CMakeLists.txt_ file on line 4 is as follows:

```
# For a new project it is sufficient to change only its name in the following line
set( PROJECT_NAME EasyMatrix )
```

That is, all we need to do is to provide the proper name of the project. The suite of _CurrencyCalc_ projects contains the _CMakeLists.txt_ files to generate the library and to generate an application linked to that library (Section 6.2).

## A.6.2 **Source Version Control and Repositories**

Even simple projects tend to grow rapidly in terms of the number of classes, functions, files, and versions. Things can become really serious if a project is conducted for years by a varying team, and in a dynamically changing environment. There are many discussions and books on the subject, but no one has a single good recipe for success. But again, there are some recommendations that can make the process a little more ordered and manageable. In this section, we discuss:

- Simultaneous work of a team of developers on a single project
- Source backups and repositories
- Project and source versioning

To facilitate these tasks, many platforms have been created and used over the years. But recently, two systems have gained significant popularity:

- *Git* – A version control tool to manage changes and maintain the history of the source code
- *GitHub* – A hosting service built on *Git* repositories. It lets us share repositories, access other users’ repositories, back up sources, and collaborate as teams

Figure A.9 shows an action diagram when working with *GitHub*. The best way to learn how to use *GitHub* is to first go through one of the tutorials available on its web page (https://github.com) and then to try to create and maintain your own test project. Needless to say, all the projects presented in this book are also available through this repo.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_620_0.png)

**Figure A.9**  Flowchart of *GitHub* operations. There is one master branch with a deployable version of the project. A branch creates a new path in a project and lets us work on different features. Each file, after being edited, changed, or deleted, is committed, so the changes and their history are saved in the repo. Pull requests start a discussion about the commits. Before merging to the master, it is possible to deploy from a branch for final testing in production. After testing and verification, the code is merged into the master branch.

Initially it is not necessary to have *Git* on the local computer, since most operations can be performed via access to the *GitHub* website. But after this first stage, it is good to install *Git* and/or to use an IDE that has built-in source-control facilities.

## 前言

深度学习正在逐步取代传统算法规整数据的能力，从自动驾驶汽车的感知到语音助手的交互，深度学习模型已经广泛应用到各个领域，这着实令人兴奋。

然而，与所有威力强大的新技术一样，深度学习也伴随着一系列新的挑战。其中最核心的挑战之一就是：如何理解和解释深度模型所做出的决策？对于人类来说，理解和解释自身行为的机制，已经是一个复杂的问题；对于一个由数百万参数构成的人工神经网络来说，这个问题就更加复杂了。

机器学习的可解释性（interpretability）正是为了应对这一挑战而提出的研究领域。它旨在开发一系列工具和方法，帮助我们窥探深度学习模型的“黑盒”内部，理解其决策过程的逻辑和依据，识别其中的潜在偏差和错误，从而建立对模型能力的信任，并进一步改进模型的设计。

本书旨在为读者提供一份深入了解机器学习可解释性领域的综合性指南。我们不仅会介绍可解释性的核心概念和经典方法，例如特征归因、显著性图谱、代理模型等，还将涵盖一些前沿的研究方向，并探讨可解释性在人工智能安全、公平性和伦理等关键议题中的作用。

我们相信，可解释性不仅是学术研究的重要课题，更是负责任地发展和应用人工智能技术的关键环节。希望本书能够帮助研究者、工程师以及所有对人工智能感兴趣的读者，建立起可解释性领域的知识框架，并激发更多有益的思考和实践。

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_622_0.png)

(a)

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_622_1.png)

(b)

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_622_2.png)

(c)

**Figure A.11** Panes with profiling results for the EasyMatrix project in the Microsoft Visual Studio IDE.  
(a) Initial profiling window. (b) Timing results after profiling. (c) Calling chain and source code of the most.

Our civilizations increasingly rely on computers and software. These days, power plants, transport, avionics, telecommunication, medicine, and many, many more industries cannot exist without properly working software. Hence, malfunctioning software is not only a matter of frustrated users who will not buy a new version of our application – in many areas, it is a matter of life or death. Therefore, throughout this book, we stress that code correctness is a primary issue in the software development process. One of the principal factors in software correctness is having well-educated software designers and programmers, continuously improving their skills. However, complete correctness is probably impossible, due to the complexity of the problems we’re trying to solve and complexity of the code itself, along with issues such as limited time, human factors, etc. Nevertheless, there are tools and methodologies that can make the situation less difficult.

Software verification can be considered at different levels. At the function level, we have shown how to use the simple C++ assert to verify logical constraints in the beginning and end of functions. This technique, which comes from the larger methodology of programming by contract, can be surprisingly simple and effective in early defect detection (Meyer 1997). Although more advanced software tools can be devised for the purpose of programming by contract, keeping things simple with the easily accessible assert is often a good trade-off. At the level of software components, such as simple classes or namespaces, we have shown how to write functions whose purpose is to verify other functions of these components. For instance, we use this approach, called unit testing, to test the correctness of conversions from decimal to Roman numbers in Section 3.17.2. These two methodologies, although simple, can have a tremendously positive impact if systematically applied in daily programming. Summarizing, they are as follows:

- Programming by contract – Programmatically checks pre- and post-conditions to functions, and class invariants in class member functions<sup>11</sup>
- Unit testing – At the simplest level, ensure the proper operation of functions and class member functions

In the rest of this section, we will present a short introduction to the automation of unit tests with an example that will let us incorporate unit tests in all our future projects. Although detailed descriptions of the domain of unit testing and the available libraries would require a longer discussion, let’s start with a list of testing frameworks and some hints for using them. The role of these frameworks is to facilitate writing unit tests but also to integrate seamlessly with projects and to allow as much automation as possible in running tests. The most popular testing libraries are as follows:
