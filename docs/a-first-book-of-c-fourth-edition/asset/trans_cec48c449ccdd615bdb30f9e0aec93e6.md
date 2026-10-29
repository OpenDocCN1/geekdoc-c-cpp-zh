

## Assignment and Interactive Input

Program errors can be detected at any of the following times:

- Before a program is compiled
- While the program is being compiled
- While the program is running
- After the program has been run and the output is being examined

The method for detecting errors before a program is compiled is called **desk checking** because you’re usually sitting at a desk with the code in front of you. It refers to the process of examining source code for syntax and logic errors. The method for detecting errors after a program has run is called **program verification and testing**.

## Compile-Time and Runtime Errors

Errors detected while a program is being compiled are called **compile-time errors**, and errors that occur while a program is running are called **runtime errors**. These terms describe when errors occur, not what caused them. Most compile-time errors, however, are caused by syntax errors, and the majority of runtime errors are caused by logic errors.

By now, you have probably encountered numerous compile-time errors. Beginning programmers tend to be frustrated by them, but experienced programmers understand the compiler is doing a lot of valuable checking, and correcting errors the compiler does detect is usually easy. Because these errors occur while a program is being developed, not while a user is performing an important task, no one but the programmer ever knows they occurred. You fix them, and they go away.

Runtime errors are more troubling because they occur while a user is running the program. Because the user in most commercial systems isn’t the programmer, typically the error can’t be assessed and corrected immediately. Runtime errors can be caused by program or hardware failures. From a programming standpoint, however, most runtime errors are caused by logic errors.

## Syntax and Logic Errors

Computer literature distinguishes between two main types of errors: syntax and logic errors. A **syntax error** is an error in ordering valid language elements in a statement or the attempt to use invalid language elements. For example, examine the following statements:

```
cout << "There are four syntax errors here\n"
cot "Can you find them";
```

They contain the following syntax errors:

- 1. A closing quotation mark is missing in line 1.
- 2. A terminating semicolon (;) is missing in line 1.
- 3. The keyword cout is misspelled in line 2.
- 4. The insertion symbol, <<, is missing in line 2.

If these errors aren’t discovered by desk checking, the compiler detects them and displays an error message.¹² Sometimes the error message is clear and the error is obvious; at other times, understanding the compiler’s error message takes a little detective work. Because

syntax errors are detected only at compile time. Strictly speaking, however, "compile time" refers to when the error is detected, and "syntax" refers to the type of error detected.

Note that the misspelling of "them" in the second statement isn't a syntax error. Although this spelling error results in displaying an undesirable output line, it's not a violation of C++'s syntax rules. It's simply a typographical error, commonly referred to as a "typo." The compiler doesn't catch this type of typographical error.

Another error the compiler doesn't catch is a logic error, which is characterized by erroneous, unexpected, or unintentional output that's a result of some flaw in the program's logic. These errors can be detected by desk checking, by program testing, by accident when a user gets erroneous output while the program is running, or not at all.

The most serious logic error is caused by not fully understanding the program's requirements because the logic in a program reflects the logic on which it's coded. For example, if a program's purpose is to calculate a mortgage payment on a house or the load-bearing strength of a steel beam and the programmer doesn't fully understand how to make the calculation, what inputs are needed to perform the calculation, or what special conditions exist (such as what happens when someone makes an extra mortgage payment or how temperature affects the beam), a logic error occurs. Because the compiler doesn't detect these errors and they often go undetected at runtime, they are always more difficult to detect than syntax errors.

If logic errors are detected, typically they're revealed in one of two main ways. First, the program executes to completion but produces incorrect results, such as the following:

- *No output*—This result is caused by omitting an output statement or using a sequence of statements that inadvertently bypasses an output statement.
- *Unappealing or misaligned output*—This result is caused by an error in an output statement.
- *Incorrect numerical results*—This result is caused by assigning incorrect values to variables in an expression, coding an incorrect or incomplete algorithm, coding a correct algorithm incorrectly, omitting a statement, making a round-off error, or using an improper sequence of statements.

Second, a logic error can cause a runtime error. Examples of this type of logic error are attempts to divide by zero or take the square root of a negative number. Typically, these errors are caused by incorrect user input. Although beginning programmers tend to blame users for runtime errors caused by entering incorrect data, professionals don't. They understand that a runtime error is a basic flaw in the program's construction that can damage the reputation of both the program and the programmer. They also understand that determining the error and correcting what caused it are more fruitful than determining who caused it.

## Testing and Debugging

Program testing should be well thought out to maximize the possibility of locating errors. In this regard, an important programming realization is that although a single test can reveal the presence of an error, it does not verify the absence of one. In other words, the fact that a

### 3.1 数据链路层协议

数据链路层协议是计算机网络中负责在相邻节点之间可靠地传输数据帧的协议。它定义了数据帧的格式、差错检测和纠正方法、流量控制机制以及介质访问控制策略。常见的数据链路层协议包括以太网（Ethernet）、点对点协议（PPP）和高级数据链路控制（HDLC）等。

#### 3.1.1 以太网协议

以太网是应用最广泛的局域网技术，它定义了物理层和数据链路层的规范。以太网帧格式包括前导码、帧起始定界符、目的地址、源地址、类型/长度字段、数据字段和帧校验序列。以太网采用CSMA/CD（载波监听多路访问/冲突检测）协议来协调多个设备对共享介质的访问。

以太网的传输速率从最初的10Mbps发展到现在的100Mbps、1Gbps、10Gbps甚至更高。现代以太网通常使用双绞线或光纤作为传输介质，并采用全双工通信模式，消除了冲突检测的需要。

#### 3.1.2 点对点协议（PPP）

点对点协议（PPP）是一种用于在两个网络节点之间建立直接连接的数据链路层协议。它广泛应用于拨号上网、宽带接入和虚拟专用网络（VPN）等场景。PPP协议提供了帧封装、链路控制协议（LCP）和网络控制协议（NCP）三大功能。

PPP帧格式包含标志字段、地址字段、控制字段、协议字段、信息字段和帧校验序列。PPP支持多种网络层协议，如IP、IPX和AppleTalk，通过NCP协议进行协商和配置。

| 协议名称 | 应用场景 | 传输介质 | 最大传输速率 |
|---------|---------|---------|------------|
| 以太网 | 局域网 | 双绞线/光纤 | 400Gbps |
| PPP | 拨号/宽带 | 电话线/光纤 | 100Mbps |
| HDLC | 广域网 | 专线 | 10Gbps |

表3-1 常见数据链路层协议对比

在选择数据链路层协议时，需要根据网络规模、传输距离、带宽需求和成本等因素进行综合考虑。以太网因其高带宽和低成本成为局域网的首选，而PPP则更适合于点对点的远程连接场景。

## Chapter 4

## Selection

- 4.1 Relational Expressions
- 4.2 The `if-else` Statement
- 4.3 Nested `if` Statements
- 4.4 The `switch` Statement
- 4.5 Common Programming Errors
- 4.6 Chapter Summary
- 4.7 Chapter Supplement: A Closer Look at Testing

![](img/202cface8244f523c2641baa2e00d7dd_156_0.png)

The term flow of control refers to the order in which a program’s statements are executed. Unless directed otherwise, the normal flow of control for all programs is sequential. This term means statements are executed in sequence, one after another, in the order in which they’re placed in the program.

Both selection and repetition statements enable programmers to alter this normal sequential flow of control. As their names imply, selection statements make it possible to select which statement, from a well-defined set, is executed next, and repetition statements make it possible to go back and repeat a set of statements. In this chapter, you learn about C++’s selection statements. Because selection requires choosing between alternatives, this chapter begins with a description of C++’s selection criteria.

## 4.1 Relational Expressions

Besides providing addition, subtraction, multiplication, and division capabilities, all computers have the capability to compare numbers. Because many seemingly “intelligent” decision-making situations can be reduced to choosing between two values, a computer’s comparison capability can be used to create a remarkable intelligence-like facility.

