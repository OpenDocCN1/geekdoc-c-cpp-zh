
this book is about learning to write code that both gets the job done now (development) and allows others to continue to get the job done in the future (maintenance). This, I have termed *practical design*.

In order to explore practical design, we need a case study. Ideally, the case study problem should be

- Large enough to be more than trivial,
- Small enough to be tractable,
- Familiar enough to not require domain specific expertise, and
- Interesting enough to maintain the reader’s attention for the duration of the book.

After taking the above criteria into consideration, I decided to select a stack-based, Reverse Polish Notation (RPN) calculator as the case study. The details of the calculator’s requirements will be defined below. I believe that the code for a fully functioning calculator is significant enough that the detailed study of its design provides

sufficient material to cover a book. Yet, the project is small enough that the book can be a reasonable length. Certainly, specialized domain expertise is not required. I suspect every reader of this book has used a calculator and is well-versed in its basic functionality. Finally, I hope that making the calculator RPN provides a suitable twist to stave off boredom.

## A Few Words About Requirements

No matter how big or how small, all programs have requirements. Requirements are those features, whether explicit or implicit, to which the program must comply. Entire books have been written on gathering and managing software requirements (see, for example, [28] or [21]). Typically, despite one’s best efforts, it is practically impossible to gather all of the requirements upfront. Sometimes, the effort required is economically infeasible. Sometimes, domain experts overlook what seem like obvious

requirements to them, and they simply neglect to relate all of their requirements to the development team. Sometimes, requirements only become apparent after the program begins to take shape. Sometimes, the customer does not understand his or her own requirements well enough to articulate them to the development team. While some of these dilemmas may be mitigated using agile development methods, the fact remains that many design decisions, some of which may have far reaching implications, must occur before all of the requirements are known.

In this book, you will not study techniques for gathering requirements; rather, the requirements are simply given upfront. Well, most of them will be given upfront. A few of the requirements have been explicitly reserved until a later chapter so that you can study how your design might change to accommodate unknown future expansion. Certainly, one could justly argue that since the author knows how the requirements will change, the initial design will correctly “predict” the unforeseen features. While this

criticism is fair, I nonetheless argue that the thought process and discussion behind the design decisions is still relevant. As a software architect, part of your job will be to anticipate future requests. Although any request is possible, incorporating too much flexibility at the outset is not economical. Designing for future expansion must always be considered as a tradeoff between the cost difference for expressly accommodating expandability upfront versus modifying the code later if a change is requested. Where a design should land in the spectrum between simplicity and flexibility must ultimately be measured against the likelihood of a feature request materializing and the feasibility of adding a new feature if its incorporation is not considered at the beginning.

## Reverse Polish Notation

I presume that anyone reading this book is familiar with the typical operation of a calculator. However, unless you grew up using a Hewlett Packard calculator, you may

be unfamiliar with how a stack-based RPN calculator functions (see [5] if you are unfamiliar with how a stack works). Simply stated, input numbers are pushed onto a stack, and operations are performed on the numbers already on the stack. A binary operator, such as addition, pops the top two numbers from the stack, adds the two numbers, and then pushes the result onto the stack. A unary operator, such as the sine function, pops one number from the top of the stack, uses this number as the operand, and pushes the result onto the stack. For those familiar with basic compiler lingo, RPN functions as the postfix notation of the operation (see [1] for a detailed discussion of postfix notation). The following list describes my opinion of just a few of the advantages of Reverse Polish Notation over conventional syntax:

- All operations can be expressed parentheses free.
- Multiple inputs and outputs can be visualized simultaneously.
- Large calculations can be trivially

decomposed into multiple, simple operations.
- Intermediate results can be trivially retained and reused.

While RPN will likely seem incredibly awkward at first, once you’ve become accustomed to it, you will curse every calculator that does not employ it when you are tasked with performing anything more complicated than simple arithmetic.

To ensure that the operation of an RPN calculator is clear, let’s examine a short example. Suppose we wish to evaluate the following expression:
(4+7)*3+2
7

On a typical, non-RPN calculator, we would type ((4 + 7) * 3 + 2)/7 and then press the = key. On an RPN calculator, we would instead type 4 7 + 3 * 2 + 7 /, where there is an enter command following each number in order to push the input onto the stack. Note that for many calculators, to reduce key entry, operations such as + may also function to

implicitly enter the previous number on the stack. Figure 1-1 shows the above calculation performed step-by-step on an RPN calculator.

operation: 4, enter 7, enter + 3, enter *
4: 4: 4: 4: 4: stack: 3:

3: 2: 2: 4 2: 2: 11 2: 1: 4 1: 7 1: 11 1: 3 1: 33

operation: / 7, enter + 2, enter
4: 4: 4: 4: stack: 3:

3: 2: 2: 35 2: 2: 33 1: 5 1: 7 1: 35 1: 2

Figure 1-1. An example calculation performed on an RPN calculator showing intermediate steps. Counterintuitively, the top of the stack is at the bottom of the screen.

## The Calculator’s Requirements

Once you understand the nature of Reverse

Polish Notation, the rest of the calculator’s functionality should be straightforward from the requirements description. If RPN is still unclear, I recommend spending some time clarifying this concept before proceeding. Given that caveat, the requirements of the calculator are now defined as follows:

- The calculator will be stack-based; the stack size should not be hard coded.
- The calculator will use RPN to perform operations.
- The calculator will exclusively operate on floating point numbers; a technique for entering input numbers (including scientific notation) should be implemented.
- The calculator will have the ability to undo and redo operations; the undo/redo stack sizes should be unlimited.
- The calculator will have the ability to swap the top two elements of the stack.
- The calculator will be able to drop (erase) an element from the top of the stack.
- The calculator will be able to clear the

entire stack.

- The calculator will be able to duplicate the element from the top of the stack.
- The calculator will be able to negate the element from the top of the stack.
- The calculator will implement the four basic arithmetic operations: addition, subtraction, multiplication, and division. Division by 0 is impermissible.
- The calculator will implement the three basic trigonometric functions and their inverses: sin, cos, tan, arcsin, arccos, and arctan. Arguments to the trigonometric functions will be given in radians.
- The calculator will implement functions for y^x and y √x.
- The calculator will implement a runtime plugin structure to expand the operations the calculator can perform.
- The calculator will implement both a command line interface (CLI) and a graphical user interface (GUI).
