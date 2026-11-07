
- Go—a board game created in China thousands of years ago⁹⁸—is widely considered one of the most complex games ever invented with 10¹⁷⁰ possible board configurations.⁹⁹ To give you a sense of how large a number that is, it’s believed that there are (only) between 10⁷⁸ and 10⁸² atoms in the known universe¹⁰⁰,¹⁰¹. In 2015, AlphaGo—created by Google’s DeepMind group—used deep learning with two neural networks to beat the European Go champion Fan Hui. Go is considered to be a far more complex game than chess. Powerful libraries enable you to use neural networks for deep learning.

- More recently, Google generalized its AlphaGo AI to create AlphaZero—a game-playing AI that *teaches itself to play other games*. In December 2017, AlphaZero learned the rules of chess and taught itself to play in less than four hours using reinforcement learning. It then beat the world champion chess program, Stockfish 8, in a 100-game match—winning or drawing every game. After *training itself* in Go for just eight hours, AlphaZero was able to play Go vs. its AlphaGo predecessor, winning 60 of 100 games.¹⁰²

## AI: A Field with Problems But No Solutions

For many decades, AI has been a field with problems and *no* solutions. That’s because once a particular problem is solved, people say, “Well, that’s not intelligence; it’s just a computer program that tells the computer exactly what to do.” However, with machine learning, deep learning and reinforcement learning, we’re not pre-programming solutions to *specific* problems. Instead, we’re letting our computers solve problems by learning from data—and, typically, lots of it. Many of the most interesting and challenging problems are being pursued with deep learning. Google alone has thousands of deep-learning projects underway.¹⁰³,¹⁰⁴

![](img/43d318ad505997c339a3ea78d716d162_105_0.png)

## Self Check

1 (Fill-In) The ultimate goal of AI is to produce a(n) ______.
Answer: artificial general intelligence.

2. **(Fill-In)** IBM’s Watson beat the two best human Jeopardy! players. Watson was trained using a combination of ________ learning and ________ learning techniques.

**Answer:** machine, reinforcement.

3. **(Fill-In)** Google’s ________ taught itself to play chess in less than four hours using reinforcement learning, then beat the world champion chess program, Stockfish 8, in a 100-game match—winning or drawing every game.

**Answer:** AlphaZero.

## Self-Review Exercises

1.1 Fill in the blanks in each of the following statements:

a) Computers process data under the control of instructions called ________.

b) A computer’s key logical units are: ________ unit, ________ unit, ________ unit, ________ unit, and ________ unit.

c) The three types of programming languages discussed in the chapter are ________, ________, and ________.

d) Programs that translate high-level-language programs into machine language are called ________.

e) ________ is an operating system for mobile devices based on the Linux kernel.

f) A(n) ________ allows a device to respond to motion.

g) C is widely known as the language of the ________ operating system.

1.2 Fill in the blanks in each of the following sentences about the C environment.

a) C programs are normally typed into a computer using a(n) ________.

b) In a C system, a(n) ________ automatically executes before the translation phase begins.

c) The ________ combines the output of the compiler with various library functions to produce an executable image.

d) The ________ transfers the executable image from disk to memory.

## Answers to Self-Review Exercises

**1.1** a) programs. b) input, output, memory, central processing, arithmetic and logic, secondary storage. c) machine languages, assembly languages, high-level languages. d) compilers. e) Android. f) accelerometer. g) UNIX.

**1.2** a) editor. b) preprocessor. c) linker. d) loader.

## Exercises

1.3 Categorize each of the following items as either hardware or software:

a) CPU.
b) C compiler.
c) ALU.
d) C preprocessor.
e) input unit.
f) an editor program.

e) One serious concern with self-driving vehicles is that they could potentially be hacked. Someone could set the speed high (or low), which could be dangerous. What if they redirect you to a destination other than what you want?

**1.8** *Research: Reproducibility* A crucial concept in data-science studies is reproducibility, which helps others (and you) reproduce your results. Research reproducibility and list the concepts used to create reproducible results in data-science studies.

**1.9** *Research: Artificial General Intelligence* One of the most ambitious goals in the field of AI is to achieve *artificial general intelligence*—the point at which machine intelligence would equal human intelligence. Research this intriguing topic. When is this forecast to happen? What are some key ethical issues this raises? Human intelligence seems to be stable over long periods. Powerful computers with artificial general intelligence could conceivably (and quickly) evolve intelligence far beyond that of humans. Research and discuss the issues this raises.

**1.10** *Research: Intelligent Assistants* Many companies now offer computerized intelligent assistants, such as IBM Watson, Amazon Alexa, Apple Siri, Google Assistant and Microsoft Cortana. Research these and others and list uses that can improve people’s lives. Research privacy and ethics issues for intelligent assistants. Locate amusing intelligent-assistant anecdotes.

**1.11** *Research: AI in Health Care* Research the rapidly growing field of AI big-data applications in health care. For example, suppose a diagnostic medical application had access to every X-ray that’s ever been taken and the associated diagnoses—that’s surely big data. “Deep Learning” computer-vision applications can work with this “labeled” data to learn to diagnose medical problems. Research deep learning in diagnostic medicine and describe some of its most significant accomplishments. What are some ethical issues of having machines instead of human doctors performing medical diagnoses? Would you trust a machine-generated diagnosis? Would you ask for a second opinion?

**1.12** *Research: Privacy and Data Integrity Legislation* In the Preface, we mentioned HIPAA (Health Insurance Portability and Accountability Act) and the California Consumer Privacy Act (CCPA) in the United States and GDPR (General Data Protection Regulation) for the European Union. Laws like these are becoming more common and stricter. Investigate each of these laws and their effects on your privacy.

**1.13** *Research: Personally Identifiable Information* Protecting users personally identifiable information (PII) is important aspect of privacy. Research and comment on this issue.

**1.14** *Research: Big Data, AI and the Cloud—How Companies Use These Technologies* For a major organization of your choice, research how they may be using each of the following technologies: AI, big data, the cloud, mobile, natural-language processing, speech recognition, speech synthesis, database, machine learning, deep learning, reinforcement learning, Hadoop, Spark, Internet of Things (IoT) and web services.

## Intro to C Programming

## 2

## Objectives

In this chapter, you'll:

- Write simple C programs.
- Use simple input and output statements.
- Use the fundamental data types.
- Learn computer memory concepts.
- Use arithmetic operators.
- Learn the precedence of arithmetic operators.
- Write simple decision-making statements.
- Begin focusing on secure C programming practices.

![](img/43d318ad505997c339a3ea78d716d162_110_0.png)

## Outline

- 2.1 Introduction
- 2.2 A Simple C Program: Printing a Line of Text
- 2.3 Another Simple C Program: Adding Two Integers
- 2.4 Memory Concepts
- 2.5 Arithmetic in C
- 2.6 Decision Making: Equality and Relational Operators
- 2.7 Secure C Programming

*Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

### 2.1 Introduction

The C language facilitates a structured and disciplined approach to computer-program design. This chapter introduces C programming and presents several examples illustrating many fundamental C features. We analyze each example one statement at a time. In Chapters 3 and 4, we introduce structured programming—a methodology that will help you produce clear, easy-to-maintain programs. We then use the structured approach throughout the remainder of the text. This chapter concludes with the first of our “Secure C Programming” sections.

### 2.2 A Simple C Program: Printing a Line of Text

We begin with a simple C program that prints a line of text. The program and its screen output are shown in Fig. 2.1.

```
// fig02_01.c
// A first program in C.
#include <stdio.h>

// function main begins program execution
int main(void) {
    printf("Welcome to C!\n");
} // end function main
```

```
Welcome to C!
```

**Fig. 2.1** | A first program in C.

### Comments

Lines 1 and 2

```
// fig02_01.c
// A first program in C.
```

begin with `//`, indicating that these two lines are comments. You insert comments to document programs and improve program readability. Comments do not cause the computer to perform actions when you execute programs—they’re simply ignored. It’s our convention in each program to use the line 1 comment to specify the file-
