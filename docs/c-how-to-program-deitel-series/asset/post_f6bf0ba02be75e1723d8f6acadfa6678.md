
- If an exception that occurs in a try block has no matching catch handler, or if an exception occurs in a statement that is not in a try block, the function that contains the statement terminates immediately, and the program attempts to locate an enclosing try block in the calling function. This process is called stack unwinding (p. 746).
- To throw an exception, use keyword `throw` followed by an operand that represents the type of the exception to throw. The operand of a throw can be of any type.

## Section 17.3 Rethrowing an Exception

- The exception handler can defer the exception handling (or perhaps a portion of it) to another exception handler. In either case, the handler achieves this by rethrowing the exception (p. 747).
- Common examples of exceptions are out-of-range array subscripts, arithmetic overflow, division by zero, invalid function parameters and unsuccessful memory allocations.

## Section 17.4 Stack Unwinding

- Unwinding the function call stack means that the function in which the exception was not caught terminates, all local variables in that function are destroyed and control returns to the statement that originally invoked that function.

## Section 17.5 When to Use Exception Handling

- Exception handling is for synchronous errors (p. 750), which occur when a statement executes.
- Exception handling is not designed to process errors associated with asynchronous events (p. 750), which occur in parallel with, and independent of, the program’s flow of control.
- As of C++11, if a function does not throw any exceptions and does not call any functions that throw exceptions, you should explicitly declare the function noexcept (p. 751).

## Section 17.6 Constructors, Destructors and Exception Handling

- Exceptions thrown by a constructor cause destructors to be called for any objects built as part of the object being constructed before the exception is thrown.
- Each automatic object constructed in a try block is destroyed before an exception is thrown.
- Stack unwinding completes before an exception handler begins executing.
- If a destructor invoked as a result of stack unwinding throws an exception, the program terminates.
- If an object has member objects, and if an exception is thrown before the outer object is fully constructed, then destructors will be executed for the member objects that have been constructed before the exception occurs.
- If an array of objects has been partially constructed when an exception occurs, only the destructors for the constructed array element objects will be called.
- When an exception is thrown from the constructor for an object that is created in a new expression, the dynamically allocated memory for that object is released.

## Section 17.7 Exceptions and Inheritance

- If a catch handler catches a reference to an exception object of a base-class type, it also can catch a reference to all objects of classes derived publicly from that base class—this allows for polymorphic processing of related errors.

## Section 17.8 Processing New Failures

- The C++ standard document specifies that, when operator new fails, it throws a bad_alloc exception (p. 752), which is defined in header <new>.
- Function set_new_handler (p. 752) takes as its argument a pointer to a function that takes no arguments and returns void. This pointer points to the function that will be called if new fails.
- Once `set_new_handler` registers a new handler (p. 754) in the program, `operator new` does not throw `bad_alloc` on failure; rather, it defers the error handling to the new-handler function.
- If `new` allocates memory successfully, it returns a pointer to that memory.

## Section 17.9 Class `unique_ptr` and Dynamic Memory Allocation

- If an exception occurs after successful memory allocation but before the `delete` statement executes, a memory leak could occur.
- The C++ Standard Library provides class template `unique_ptr` (p. 755) to deal with memory leaks.
- An object of class `unique_ptr` maintains a pointer to dynamically allocated memory. A `unique_ptr`’s destructor performs a delete operation on the `unique_ptr`’s pointer data member.
- Class template `unique_ptr` provides overloaded operators `*` and `->` so that a `unique_ptr` object can be used just as a regular pointer variable is. A `unique_ptr` also transfers ownership of the dynamic memory it manages via its copy constructor and overloaded assignment operator.

## Section 17.10 Standard Library Exception Hierarchy

- The C++ Standard Library includes a hierarchy of exception classes. This hierarchy is headed by base-class `exception`.
- Immediate derived classes of base class `exception` include `runtime_error` and `logic_error` (both defined in header `<stdexcept>`), each of which has several derived classes.
- Several operators throw standard exceptions—`operator new` throws `bad_alloc`, `operator dynamic_cast` throws `bad_cast` (p. 758) and `operator typeid` throws `bad_typeid` (p. 758).

## Self-Review Exercises

- 17.1  List five common examples of exceptions.
- 17.2  Give several reasons why exception-handling techniques should not be used for conventional program control.
- 17.3  Why are exceptions appropriate for dealing with errors produced by library functions?
- 17.4  What’s a “resource leak”?
- 17.5  If no exceptions are thrown in a `try` block, where does control proceed to after the `try` block completes execution?
- 17.6  What happens if an exception is thrown outside a `try` block?
- 17.7  Give a key advantage and a key disadvantage of using `catch(...)`.
- 17.8  What happens if no `catch` handler matches the type of a thrown object?
- 17.9  What happens if several handlers match the type of the thrown object?
- 17.10  Why would you specify a base-class type as the type of a `catch` handler, then throw objects of derived-class types?
- 17.11  Suppose a `catch` handler with a precise match to an exception object type is available. Under what circumstances might a different handler be executed for exception objects of that type?
- 17.12  Must throwing an exception cause program termination?
- 17.13  What happens when a `catch` handler throws an exception?
- 17.14  What does the statement `throw;` do?

## 高端对话：网络智能体的发展与安全

当前，网络智能体（AI Agent）正在重塑网络空间格局，成为数字经济时代的关键基础设施。其安全性与可信性也将直接关系到个人隐私、企业核心资产乃至国家关键信息基础设施的整体安全。人工智能技术的快速演进给网络智能体的安全治理带来了哪些新挑战？企业应当采取何种措施构建安全、可靠的网络智能体？如何协同推动网络智能体的安全标准与生态建设？围绕以上热点议题，本刊邀请业界专家深入探讨，共同展望网络智能体的未来发展趋势。

本期对话嘉宾

- **李万鹏** 中国信息通信研究院安全研究所副所长
- **王昊** 华为技术有限公司网络安全首席专家
- **陈飞** 百度安全副总经理
- **刘洋** 奇安信科技集团股份有限公司安全专家

主持人：本刊记者 张某某

中国信息安全：请您谈谈当前网络智能体发展面临的主要安全挑战有哪些？

> **李万鹏**：随着大模型能力不断增强，网络智能体在自主决策、工具调用、多智能体协同等场景中展现出巨大潜力。但与此同时，模型幻觉、提示注入、工具滥用、数据泄露等新型安全风险也日趋突出。此外，网络智能体的行为具有一定的不可预测性，其安全治理面临更大的不确定性。

- **17.18**  *(Exception Handling vs. Other Schemes)* Compare and contrast exception handling with the various other exception-processing schemes discussed in the text.
- **17.19**  *(Exception Handling and Program Control)* Why should exceptions *not* be used as an alternative form of program control?
- **17.20**  *(Handling Related Exceptions)* Describe a technique for handling related exceptions.
- **17.21**  *(Throwing Exceptions from a catch)* Suppose a program throws an exception and the appropriate exception handler begins executing. Now suppose that the exception handler itself throws the same exception. Does this create infinite recursion? Write a program to check your observation.
- **17.22**  *(Catching Derived-Class Exceptions)* Use inheritance to create various derived classes of `runtime_error`. Then show that a catch handler specifying the base class can catch derived-class exceptions.
- **17.23**  *(Throwing the Result of a Conditional Expression)* Throw the result of a conditional expression that returns either a double or an int. Provide an int catch handler and a double catch handler. Show that only the double catch handler executes, regardless of whether the int or the double is returned.
- **17.24**  *(Local Variable Destructors)* Write a program illustrating that all destructors for objects constructed in a block are called before an exception is thrown from that block.
- **17.25**  *(Member Object Destructors)* Write a program illustrating that member object destructors are called for only those member objects that were constructed before an exception occurred.
- **17.26**  *(Catching All Exceptions)* Write a program that demonstrates several exception types being caught with the `catch(...)` exception handler.
- **17.27**  *(Order of Exception Handlers)* Write a program illustrating that the order of exception handlers is important. The first matching handler is the one that executes. Attempt to compile and run your program two different ways to show that two different handlers execute with two different effects.
- **17.28**  *(Constructors Throwing Exceptions)* Write a program that shows a constructor passing information about constructor failure to an exception handler after a try block.
- **17.29**  *(Rethrowing Exceptions)* Write a program that illustrates rethrowing an exception.
- **17.30**  *(Uncaught Exceptions)* Write a program that illustrates that a function with its own try block does not have to catch every possible error generated within the try. Some exceptions can slip through to, and be handled in, outer scopes.
- **17.31**  *(Stack Unwinding)* Write a program that throws an exception from a deeply nested function and still has the catch handler following the try block enclosing the initial call in main catch the exception.
