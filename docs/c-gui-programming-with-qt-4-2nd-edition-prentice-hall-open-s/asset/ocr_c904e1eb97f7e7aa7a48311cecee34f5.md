# 2. Application Scripting

![](bbox=[0.012, 0.053, 0.381, 0.193])

+   - Overview of the ECMAScript Language
- Extending Qt Applications with Scripts
- Implementing GUI Extensions Using Scripts
- Automating Tasks through Scripting

Scripts are programs written in an interpreted language that extend the facilities of an existing system. Some scripts are run as stand-alone applications, whereas others execute embedded in applications. Qt includes QtScript, a module that can be used to make Qt applications scriptable using ECMAScript, the standardized version of JavaScript. This module is a complete rewrite of the earlier Trolltech Qt Script for Applications (QSA) and provides full support for ECMAScript Edition 3.

ECMAScript is the official name of the language standardized by Ecma International. It forms the basis of JavaScript (Mozilla), JScript (Microsoft), and ActionScript (Adobe). Although the language's syntax is superficially similar to C++ and Java, the underlying concepts are radically different and set it apart from most other object-oriented-programing languages. In the first section of this chapter, we will quickly review the ECMAScript language and show how to run ECMAScript code using Qt. If you already know JavaScript or any other ECMAScript-based language, you can just skip this section.

In the second section, we will see how to add scripting support to a Qt application. This makes it possible for users to add their own functionality in addition to what the application already provides. This approach is also frequently used to make it easier to support users; technical staff can supply bug fixes and workarounds in the form of scripts.

In the third section, we will show how to develop GUI front-ends and forms created using Qt Designer. This technique is appealing to developers who dislike the "compile, link, run" cycle associated with C++ development and prefer the scripting approach. It also enables users with JavaScript experience to design fully functional GUI interfaces without having to learn C++.