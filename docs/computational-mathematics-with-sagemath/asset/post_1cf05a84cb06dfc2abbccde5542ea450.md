
## Part I Getting to Grips with Sage

## 1 First Steps

This introductory chapter presents the way the Sage mathematical system thinks. The next chapters of this first part develop the basic notions: how to make symbolic or numerical computations in analysis, how to work with vectors or matrices, write programs, deal with data lists, produce graphics, etc. The following parts of this book treat in more detail some branches of mathematics where computers are very helpful.

### 1.1 The Sage Program

#### 1.1.1 A Tool for Mathematics

Sage is a piece of software implementing mathematical algorithms in a variety of contexts. To start with, it can be used as a scientific pocket calculator, and can manipulate all sorts of numbers, from integers and rational numbers to numerical approximations of real and complex numbers with arbitrary precision, and also including elements of finite fields.

However, mathematical computations go far beyond numbers: Sage is a *computer algebra system*; it can for example help junior high school students learn how to solve linear equations, or develop, factor, or simplify expressions; or carry out such operations in arbitrary rings of polynomials or rational function fields. In analysis, Sage can manipulate expressions involving square roots, exponentials, logarithms or trigonometric functions: integration, computation of limits, simplification of sums, series expansion, solution of certain differential equations, and more. In linear algebra it computes with vectors, matrices, and subspaces. It can also help illustrate and solve problems in probability, statistics, and combinatorics.

To summarise, Sage strives to provide a consistent and uniform access to features in a wide area of mathematics — ranging from group theory to numerical analysis — and beyond — visualisation in two and three dimensions, animation, networking, databases, ... Using a single unified piece of software frees the (budding) mathematician from having to transfer data between several tools and learn the syntax of several programming languages.

### Access to Sage

To use Sage, all that is needed is a web browser. As a starter, the service http://sagecell.sagemath.org/ allows for testing commands. To go further, one can use one of the online services. For example, CoCalc (http://cocalc.com, formerly known as SageMathCloud) gives access to a lot of computational software and collaborative tools, together with course management features. Developed and hosted by SageMath Inc., an independent company founded by William Stein, its access is free for casual use, and most of its code is free. Other similar services are hosted by universities and institutions. Ask around to find out what is available near you.

For regular usage, it is recommended to use Sage on one’s own machine, installing it if this has not yet been done by the system administrator. Sage is available for most operating systems: Linux, Windows, MacOS; see the Download section on http://sagemath.org.

How to start Sage depends on the environment; therefore we do not go into details here. On CoCalc one needs to create an account, a project, and finally a Jupyter worksheet. On a desktop, the system may provide a startup icon. Under Linux or MacOS, one typically would launch the command `sage --notebook jupyter` in a terminal.

### Resources

The official Sage website offers many resources:

- http://www.sagemath.org/ — official site
- http://doc.sagemath.org/ — documentation
- http://wiki.sagemath.org/quickref — command lists

To get help on using Sage, the Question and Answer site http://ask.sagemath.org/ is very active. For technical questions (installation, troubleshooting, ...), the best medium is the mailing list sage-support@googlegroups.com.

### User interfaces: notebooks or command line

However Sage is accessed, one can use it via a web application enabling the editing and sharing of notebooks which mix code, interactive computations, equations, visualisations and text:

![](img/99840d73c45ee58b635c4eedc727fd9a_18_0.png)

The Help menu gives access to the documentation. We recommend starting with the User Interface Tour, returning often to the Keyboard Shortcuts, and progressively exploring the Thematic Tutorials.

Sage uses Jupyter as a web application. Formerly known as IPython, Jupyter allows the use of a great deal of mathematical software (GAP, PARI/GP, or Singular, ...) and beyond (from Python to C++!), and is supported by a large community. Notebooks are respectively in the .sws and .ipynb format. CoCalc offers another format .sagenb which is less portable, but exploits advanced interaction features.

As an alternative, one can use Sage in a terminal. Its calculator-like command line interface gives full access to all of its capabilities, including graphics:

![](img/99840d73c45ee58b635c4eedc727fd9a_18_1.png)

### Sage and Python

Like most software for mathematical computations, Sage is used by issuing commands written in a programming language. For this purpose, Sage uses the general purpose programming language Python, with just a tiny layer of syntactic sugar to support some common mathematical notations in interactive use. For complicated or just repetitive calculations, one can write programs instead of simple one-line commands. When mature and of general interest, such programs can be submitted for inclusion in Sage.

### Aims and history of Sage

In 2005, William Stein, an American academic, initiated the Sage project, with the goal of producing free software for mathematical computation, developed by users for users. This meets a longstanding need of mathematicians, and soon an international community of hundreds of developers crystallised around Sage, most of them teachers and researchers. At first Sage had some focus on number theory, the area of interest of its founder. As contributions flowed in, its capabilities progressively extended to many areas of mathematics. This, together with the numerical capabilities brought in by the Scientific Python ecosystem, has made Sage the general purpose mathematics software that it is today.

Not only can Sage be used and downloaded for free, but it is free software: the authors impose no restriction on its usage, redistribution, study or modification, as long as the modifications are free themselves. In the same spirit, the material in this book can be freely read, shared, and reused (with proper credit, of course). This license is in harmony with the spirit of free development and dissemination of knowledge in academia.

### Sage, a software in an ecosystem

The development of Sage was relatively quick thanks to its strategy of reusing existing free software, including many specialised mathematical libraries or systems like GAP, PARI/GP, Maxima, Singular, to cite just a few.

Sage itself is written in Python, a programming language used by millions and known for the ease with which it can be learned. Python is particularly well established in the sciences. Within the same computing environment, it is possible to combine the capabilities of Sage with scientific libraries for numerical computations, data analysis, statistics, visualisation, machine learning, biology, astrophysics, and technical libraries for networking, databases, web, ... See for example: https://en.wikipedia.org/wiki/List_of_Python_software.

### SAGE, Sage, or SageMath?

![](img/99840d73c45ee58b635c4eedc727fd9a_20_0.png)

**FIGURE 1.1** — The first occurrence of the name Sage, on a handwritten note of W. Stein.

At first, Sage was both an acronym and a reference to the “sage” medicinal plant. When the system later expanded to cover much of mathematics, the acronym part was dropped. As Sage came to be known in larger circles, and to avoid confusion with, for example, the business management software of the same name, the official name was changed to SageMath. When the context is unambiguous, for example in this book, it is traditional to just use Sage.

### 1.2 Sage as a Calculator

#### 1.2.1 First Computations

In the rest of the book, we present computations in the following form, which mimics a command line Sage session:

```
sage: 1+1
2
```

The `sage:` text in the beginning of the first line is the command prompt of the system. The prompt (which does not appear in the notebook interface) means that Sage awaits a user command. The rest of the line is the command to execute, which is validated with the ⟨Enter⟩ key. The lines below are the system’s answer, which in general are the results of the computation. Some commands use several lines (see Chapter 3). The additional command lines can then be recognised by `...` at the beginning of the line. A multi-line command should follow the position of linebreaks and the indentation (spaces to align the line with respect to the previous one), without copying the initial `...`.

In the notebook, one directly enters the commands in a computation cell, and validates by clicking on *evaluate* or using the ⟨Shift⟩+⟨Enter⟩ key combination. The combination ⟨Alt⟩+⟨Enter⟩ not only executes the command of the current cell, but also creates a new cell just below. One can also create a new cell by clicking in the small space just above a given cell, or below the last cell.

Sage interprets simple formulas like a scientific calculator. The operations +, ×, etc. have their usual precedence, and parentheses their common usage:
