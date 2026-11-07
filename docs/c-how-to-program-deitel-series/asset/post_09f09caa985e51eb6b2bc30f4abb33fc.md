
## 4.4 Control Structures

Normally, statements in a program execute one after the other in the order in which they’re written. This is called **sequential execution**. Various C++ statements we’ll soon discuss enable you to specify that the *next* statement to execute may be other than the next one in sequence. This is called **transfer of control**.

During the 1960s, it became clear that the indiscriminate use of transfers of control was the root of much difficulty experienced by software development groups. Blame was pointed at the **goto statement**, which allows you to specify a transfer of control to one of a wide range of possible destinations in a program (creating what’s often called “spaghetti code”). The notion of so-called **structured programming** became almost synonymous with “**goto elimination**.”

The research of Böhm and Jacopini demonstrated that programs could be written *without any* `goto` statement. It became the challenge of the era for programmers to shift their styles to “goto-less programming.” It was not until the 1970s that programmers started taking structured programming seriously. The results have been impressive, as software development groups have reported reduced development times, more frequent on-time delivery of systems and more frequent within-budget completion of software projects. The key to these successes is that structured programs are clearer, easier to debug, test and modify and more likely to be bug-free in the first place.

Böhm and Jacopini’s work demonstrated that all programs could be written in terms of only three **control structures**, namely, the **sequence structure**, the **selection structure** and the **repetition structure**. The term “control structures” comes from the field of computer science. When we introduce C++’s implementations of control structures, we’ll refer to them in the terminology of the C++ standard document as “control statements.”

### Sequence Structure in C++

The *sequence structure* is built into C++. Unless directed otherwise, the computer executes C++ statements one after the other in the order in which they’re written—that is, in sequence. The UML activity **diagram** of Fig. 4.2 illustrates a typical sequence structure in

![](img/b42ba5cd262b1358d16610173f975e4d_142_0.png)

**Fig. 4.2** | Sequence-structure activity diagram.

1. Böhm, C., and G. Jacopini, “Flow Diagrams, Turing Machines, and Languages with Only Two Formation Rules,” *Communications of the ACM*, Vol. 9, No. 5, May 1966, pp. 366–371.

called a **double-selection statement** because it selects between two different actions (or groups of actions). The switch selection statement is called a **multiple-selection statement** because it selects among many different actions (or groups of actions).

### Repetition Statements in C++

C++ provides three types of repetition statements (also called **looping statements** or **loops**) for performing statements repeatedly while a condition (called the **loop-continuation condition**) remains true. These are the **while**, **do...while** and **for** statements. (Chapter 5 presents the do...while and for statements, and Chapter 7 presents a specialized version of the for statement that’s used with so-called arrays and containers.) The while and for statements perform the action (or group of actions) in their bodies zero or more times—if the loop-continuation condition is initially false, the action (or group of actions) will **not** execute. The do...while statement performs the action (or group of actions) in its body at **least once**.

Each of the words if, else, switch, while, do and for is a C++ keyword. Keywords **cannot** be used as identifiers, such as variable names, and must be spelled with only lowercase letters. Figure 4.3 provides a complete list of C++ keywords.

| C++ Keywords |  |  |  |  |
|---|---|---|---|---|
| *Keywords common to the C and C++ programming languages* |  |  |  |  |
| auto | break | case | char | const |
| continue | default | do | double | else |
| enum | extern | float | for | goto |
| if | int | long | register | return |
| short | signed | sizeof | static | struct |
| switch | typedef | union | unsigned | void |
| volatile | while |  |  |  |
| *C++-only keywords* |  |  |  |  |
| and | and_eq | asm | bitand | bitor |
| bool | catch | class | compl | const_cast |
| delete | dynamic_cast | explicit | export | false |
| friend | inline | mutable | namespace | new |
| not | not_eq | operator | or | or_eq |
| private | protected | public | reinterpret_cast | static_cast |
| template | this | throw | true | try |
| typeid | typename | using | virtual | wchar_t |
| xor | xor_eq |  |  |  |
| *C++11 keywords* |  |  |  |  |
| alignas | alignof | char16_t | char32_t | constexpr |
| decltype | noexcept | nullptr | static_assert | thread_local |

**Fig. 4.3** | C++ keywords.

Figure 4.4 illustrates the single-selection if statement. It contains what is perhaps the most important symbol in an activity diagram—the diamond or **decision symbol**, which indicates that a *decision* is to be made. A decision symbol indicates that the workflow will continue along a path determined by the symbol’s associated **guard conditions**, which can be true or false. Each transition arrow emerging from a decision symbol has a guard condition specified in *square brackets* above or next to the transition flow. If a particular guard condition is true, the workflow enters the action state to which that transition arrow points. In Fig. 4.4, if the grade is greater than or equal to 60, the program prints “Passed” to the screen, then transitions to the final state of this activity. If the grade is less than 60, the program immediately transitions to the final state without displaying a message.

![](img/b42ba5cd262b1358d16610173f975e4d_146_0.png)

**Fig. 4.4** | *if* single-selection statement activity diagram.

You saw in Chapter 2 that decisions can be based on conditions containing relational or equality operators. Actually, in C++, a decision can be based on *any* expression—if the expression evaluates to zero, it’s treated as *false*; if the expression evaluates to *nonzero*, it’s treated as *true*. C++ provides the data type **bool** for variables that can hold only the values **true** and **false**—each of these is a C++ keyword.

> **Portability Tip 4.1**
>
> For compatibility with earlier versions of C, which used integers for Boolean values, the bool value true also can be represented by any nonzero value (compilers typically use 1) and the bool value false also can be represented as the value zero.

The if statement is a *single-entry/single-exit* statement. We’ll see that the activity diagrams for the remaining control statements also contain initial states, transition arrows, action states that indicate actions to perform, decision symbols (with associated guard conditions) that indicate decisions to be made and final states.

Envision seven bins, each containing only empty UML activity diagrams of one of the seven types of control statements. Your task, then, is assembling a program from the activity diagrams of as many of each type of control statement as the algorithm demands, combining the activity diagrams in only two possible ways (stacking or nesting), then filling in the action states and decisions with action expressions and guard conditions in a manner appropriate to form a structured implementation for the algorithm. We’ll continue discussing the variety of ways in which actions and decisions may be written.

## 4.6 `if...else` Double-Selection Statement

The `if` single-selection statement performs an indicated action only when the condition is true; otherwise the action is skipped. The `if...else` double-selection statement allows you to specify an action to perform when the condition is true and a different action to perform when the condition is false. For example, the pseudocode statement

```
If student's grade is greater than or equal to 60
    Print "Passed"
Else
    Print "Failed"
```

prints “Passed” if the student’s grade is greater than or equal to 60, but prints “Failed” if the student’s grade is less than 60. In either case, after printing occurs, the next pseudocode statement in sequence is “performed.”

The preceding `If...Else` statement can be written in C++ as

```
if ( grade >= 60 )
    cout << "Passed";
else
    cout << "Failed";
```

The body of the else is also indented.

> **Good Programming Practice 4.1**
>
> *If there are several levels of indentation, each level should be indented the same additional amount of space to promote readability and maintainability.*

Figure 4.5 illustrates the `if...else` statement’s flow of control.

![](img/b42ba5cd262b1358d16610173f975e4d_147_0.png)

**Fig. 4.5** | `if...else` double-selection statement activity diagram.
