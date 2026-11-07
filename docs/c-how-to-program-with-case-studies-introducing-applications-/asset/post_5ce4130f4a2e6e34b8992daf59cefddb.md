
- We adhere to the C11/C18 standards.

- We tested all the code for correctness on the **Windows, macOS and Linux** operating systems using the latest versions of the **Visual C++, Xcode and GNU gcc compilers**, respectively, notifying differences among the platforms. See the **Before You Begin** section that follows this Preface for software installation instructions.

- We used the **clang-tidy static code analysis tool** to check all the code in the book’s code examples for improvement suggestions, from simple items like **ensuring variables are initialized to warnings about potential security flaws**. We also ran this tool on the code solutions that we make available to instructors for hundreds of the book’s exercises. The complete list of code checks can be found at https://clang.llvm.org/extra/clang-tidy/checks/list.html.

- GNU gcc tends to be the most compliant C compiler. To enable **macOS and Windows users to use gcc** if they wish, **Chapter 1 includes a test-drive demonstrating how to compile programs and run them using gcc in the cross-platform GNU Compiler Collection Docker container.**

- We’ve added 350+ integrated Self-Check exercises, each followed immediately by its answer. These are ideal for self study and for use in **“flipped classrooms”** (see the “Flipped Classrooms” section later in this Preface).

- To ensure that book content is **topical**, we did extensive Internet research on C specifically and the world of computing in general, which influenced our choice of case studies. We show C as it’s intended to be used with a rich collection of applications programming and systems programming case studies, focusing on **computer-science, artificial intelligence, data science** and other fields. See the “Case Studies” section later in this Preface for more details.

- In the text, code examples, exercises and case studies, we familiarize students with **current topics of interest to developers**, including open-source software, virtualization, simulation, web services, multithreading, multicore hardware architecture, systems programming, game programming, animation, visualization, 2D and 3D graphics, artificial intelligence, natural language processing, machine learning, robotics, data science, secure programming, cryptography, Docker, GitHub, StackOverflow, forums and more.

- We adhere to the latest **ACM/IEEE computing curricula recommendations**, which call for covering security, data science, ethics, privacy and performance concepts and using real-world data throughout the curriculum. See the “Computing and Data Science Curricula” section for more details.

- Most chapters in this book’s recent editions end with **Secure C programming sections** that focus on the SEI CERT C Coding Standard from the CERT group of Carnegie Mellon University’s Software Engineering Institute (SEI). For this edition, we tuned the SEI CERT-based sections. We also added **security icons in the page margin** whenever we discuss a security-related issue in the text. All of this is consistent with the **ACM/IEEE computing curricula documents’** enhanced emphasis on security. See the “Computing and Data Science Curricula” section later in this Preface for a list of the key curricula documents.

- Consistent with our richer treatment of security, we’ve added case studies on secret-key and public-key cryptography. The latter includes a detailed walk-through of the enormously popular RSA algorithm’s steps, providing hints to help you build a working, simple, small-scale implementation.

- We’ve enhanced existing case studies and added new ones focusing on AI and data science, including simulations with random-number generation, survey data analysis, natural language processing (NLP) and artificial intelligence (machine-learning with simple linear regression). Data science is emphasized in the latest ACM/IEEE computing curricula documents.

- We’ve added exercises in which students use the Internet to research ethics and privacy issues in computing.

- We tuned our multithreading and multicore performance case study. We also show a performance icon in the margin whenever we discuss a performance-related issue in the text.

- We integrated the previous edition’s hundreds of software-development tips directly into the text for a smoother reading experience. We call out common errors and good software engineering practices with new margin icons.

- We upgraded our appendix on additional sorting algorithms and analysis of algorithms with Big O to full-chapter status (Chapter 13).

- C programmers often subsequently learn one or more C-based object-oriented languages. We added an appendix that presents a friendly intro to object-oriented programming concepts and terminology. C is a procedural programming language, so this appendix will help students appreciate differences in thinking between C developers and the folks who program in languages like C++, Java, C#, Objective-C, Swift and other object-oriented languages. We do lots of things like this in the book to prepare students for industry.

- Several case studies now have you use free open-source libraries and tools.

- We added a case study that performs visualization with gnuplot.

- We removed the previous edition’s introduction to C++ programming to make room for the hundreds of integrated self-check exercises and our new applications programming and systems programming case studies.

- This new edition is published in a larger font size and page size for enhanced readability.

## A Tour of the Book

The Table of Contents graphic on the inside front cover shows the book’s modular architecture. Instructors can conveniently adapt the content to a variety of courses and audiences. Here we present a brief chapter-by-chapter walkthrough and indicate where
the book’s case studies are located. Some are in-chapter examples and some are end-of-chapter exercises. Some are fully coded. For others, you’ll develop the solution.

Chapters 1–5 are traditional introductory C programming topics. Chapters 6–11 are intermediate topics forming the high end of Computer Science 1 and related courses. Chapters 12–15 are advanced topics for late CS1 or early CS2 courses. Here’s a list of the topical, challenging and often entertaining hands-on case studies.

## Systems Programming Case Studies

- Systems Software—Building Your Own Computer (as a virtual machine)
- Systems Software—Building Your Own Compiler
- Embedded Systems Programming—Robotics, 3D graphics and animation with the Webots Simulator
- Performance with Multithreading and Multicore Systems

## Application Programming Case Studies

- Algorithm Development—Counter-Controlled Iteration
- Algorithm Development—Sentinel-Controlled Iteration
- Algorithm Development—Nested Control Statements
- Random-Number Simulation—Building a Casino Game
- Random-Number Simulation—Card Shuffling and Dealing
- Random-Number Simulation—The Tortoise and the Hare Race
- Intro to Data Science—Survey Data Analysis
- Direct-Access File Processing—Building a Transaction-Processing System
- Visualizing Searching and Sorting Algorithms—Binary Search and Merge Sort.
- Artificial Intelligence/Data Science—Natural Language Processing (“Who Really Wrote the Works of William Shakespeare?”)
- Artificial Intelligence/Data Science—Machine Learning with the GNU Scientific Library (“Statistics Can Be Deceiving” and “Have Average January Temperatures in New York City Been Rising Over the Last Century?”)
- Game Programming—Cannon Game with the raylib Library
- Game Programming—SpotOn Game with the raylib Library
- Multimedia: Audio and Animation—The Tortoise and the Hare Race with the raylib Library
- Security and Cryptography—Implementing a Vigenère Secret-Key Cipher and RSA Public-Key Cryptography
- Animated Visualization with raylib—The Law of Large Numbers
- Web Services and the Cloud—Getting a Weather Report Using libcurl and the OpenWeatherMap Web Services, and An Introduction to Building Mashups with Web Services.
