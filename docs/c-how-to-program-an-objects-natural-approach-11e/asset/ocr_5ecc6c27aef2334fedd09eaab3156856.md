# Outline

+   - **16.1** Introduction
+   - **16.2** Compilation and Linking Before C++20
+   - **16.3** Advantages and Goals of Modules
+   - **16.4** Example: Transitioning to Modules—Header Units
+   - **16.5** Modules Can Reduce Translation Unit Sizes and Compilation Times
+   - **16.6** Example: Creating and Using a Module
+     - 16.6.1 `module` Declaration for a Module Interface Unit
+     - 16.6.2 Exporting a Declaration
+     - 16.6.3 Exporting a Group of Declarations
+     - 16.6.4 Exporting a namespace
+     - 16.6.5 Exporting a namespace Member
+     - 16.6.6 Importing a Module to Use Its Exported Declarations
+     - 16.6.7 Example: Attempting to Access Non-Exported Module Contents
+   - **16.7** Global Module Fragment
+   - **16.8** Separating Interface from Implementation
+     - 16.8.1 Example: Module Implementation Units
+     - 16.8.2 Example: Modularizing a Class
+     - 16.8.3 `:private` Module Fragment
+   - **16.9** Partitions
+     - 16.9.1 Example: Module Interface Partition Units
+     - 16.9.2 Module Implementation Partition Units
+     - 16.9.3 Example: “Submodules” vs. Partitions
+   - **16.10** Additional Modules Examples
+     - 16.10.1 Example: Implementing the C++ Standard Library as Modules
+     - 16.10.2 Example: Cyclic Dependencies Are Not Allowed
+     - 16.10.3 Example: `imports` Are Not Transitive
+     - 16.10.4 Example: Visibility vs. Reachability
+   - **16.11** Migrating Code to Modules
+   - **16.12** Future of Modules and Modules Tooling
+   - **16.13** Wrap-Up
+   - Exercises
+   - Appendix: Modules Videos Bibliography
+   - Appendix: Modules Articles Bibliography
+   - Appendix: Modules Glossary

# ## 16.1 Introduction

Modules—one of C++20’s “big four” features (along with ranges, concepts and coroutines)—provide a new way to organize your code, precisely control which declarations you expose to client code and encapsulate implementation details.¹ Each module is a uniquely named, reusable group of related declarations and definitions with a well-defined interface that client code can use.

This chapter presents many complete, working code examples that introduce modules. Modules help developers be more productive, especially as they build, maintain and evolve large software systems.² Modules also aim to make such systems more scalable.³ C++ creator Bjarne Stroustrup says, “Modules offer a historic opportunity to improve code hygiene and compile times for C++ (bringing C++ into the 21st century).”⁴

![](bbox=[0.113, 0.622, 0.179, 0.649])

+   1. Daveed Vandevoorde, “Modules in C++ (Revision 6),” January 11, 2012. Accessed April 18, 2023. https://wg21.link/n3347.
+   2. Gabriel Dos Reis, “Programming in the Large with C++20: Meeting C++ 2020 Keynote,” December 11, 2020. Accessed April 18, 2023. https://www.youtube.com/watch?v=j4du4LNsLiI.
+   3. Vassil Vassilev¹, David Lange¹, Malik Shahzad Muzaffar, Mircho Radozov, Oksana Sadhana and Alexander Penev, “C++ Modules in ROOT and Beyond,” August 25, 2020. Accessed April 18, 2023. https://indico.cern.ch/event/2004.06507.pdf.
+   4. Bjarne Stroustrup, “Modules and Macros,” February 11, 2018. Accessed April 18, 2023. https://wg21.link/p0955r0.