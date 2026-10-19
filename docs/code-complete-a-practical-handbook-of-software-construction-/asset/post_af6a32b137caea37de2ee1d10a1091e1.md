
## Call an error-processing routine/object

Another approach is to centralize error handling in a global error-handling routine or error-handling object. The advantage of this approach is that error-processing responsibility can be centralized, which can make debugging easier. The tradeoff is that the whole program will know about this central capability and will be coupled to it. If you ever want to reuse any of the code from the system in another system, you’ll have to drag the error-handling machinery along with the code you reuse.

This approach has an important security implication. If your code has encountered a buffer overrun, it’s possible that an attacker has compromised the address of the handler routine or object. Thus, once a buffer overrun has occurred while an application is running, it is no longer safe to use this approach.

## Display an error message wherever the error is encountered

This approach minimizes error-handling overhead; however, it does have the potential to spread user interface messages through the entire application, which can create challenges when you need to create a consistent user interface, when you try to clearly separate the UI from the rest of the system, or when you try to localize the software into a different language. Also, beware of telling a potential attacker of the system too much. Attackers sometimes use error messages to discover how to attack a system.

## Handle the error in whatever way works best locally

Some designs call for handling all errors locally—the decision of which specific error-handling method to use is left up to the programmer designing and implementing the part of the system that encounters the error.

This approach provides individual developers with great flexibility, but it creates a significant risk that the overall performance of the system will not satisfy its requirements for correctness or robustness (more on this in a moment). Depending on how developers end up handling specific errors, this approach also has the potential to spread user interface code throughout the system, which exposes the program to all the problems associated with displaying error messages.

## Shut down

Some systems shut down whenever they detect an error. This approach is useful in safety-critical applications. For example, if the software that controls radiation equipment for treating cancer patients receives bad input data for the radiation dosage, what is its best error-handling response? Should it use the same value as last time? Should it use the closest legal value? Should it use a neutral value? In this case, shutting down is the best option. We’d much prefer to reboot the machine than to run the risk of delivering the wrong dosage.

A similar approach can be used to improve the security of Microsoft Windows. By default, Windows continues to operate even when its security log is full. But you can configure Windows to halt the server if the security log becomes full, which can be appropriate in a security-critical environment.

## 8.4 Exceptions

Exceptions are a specific means by which code can pass along errors or exceptional events to the code that called it. If code in one routine encounters an unexpected condition that it doesn’t know how to handle, it throws an exception, essentially throwing up its hands and yelling, “I don’t know what to do about this—I sure hope somebody else knows how to handle it!” Code that has no sense of the context of an error can return control to other parts of the system that might have a better ability to interpret the error and do something useful about it.

Exceptions can also be used to straighten out tangled logic within a single stretch of code, such as the “Rewrite with try-finally” example in Section 17.3. The basic structure of an exception is that a routine uses throw to throw an exception object. Code in some other routine up the calling hierarchy will catch the exception within a try-catch block.

Popular languages vary in how they implement exceptions. Table 8-1 summarizes the major differences in three of them:

## Table 8-1 Popular-Language Support for Exceptions

| Exception Attribute | C++ | Java | Visual Basic |
|---|---|---|---|
| Try-catch support | yes | yes | yes |
| Try-catch-finally support | no | yes | yes |
| What can be thrown | Exception object or object derived from Exception class; object pointer; object reference; data type like string or int | Exception object or object derived from Exception class | Exception object or object derived from Exception class |
| Effect of uncaught exception | Invokes std::unexpected(), which by default invokes std::terminate(), which by default invokes abort() | Terminates thread of execution if exception is a “checked exception”; no effect if exception is a “runtime exception” | Terminates program |
| Exceptions thrown must be defined in class interface | No | Yes | No |
| Exceptions caught must be defined in class interface | No | Yes | No |

> Programs that use exceptions as part of their normal processing suffer from all the readability and maintainability problems of classic spaghetti code.
> —Andy Hunt and Dave Thomas

Exceptions have an attribute in common with inheritance: used judiciously, they can reduce complexity. Used imprudently, they can make code almost impossible to follow. This section contains suggestions for realizing the benefits of exceptions and avoiding the difficulties often associated with them.

## Use exceptions to notify other parts of the program about errors that should not be ignored

The overriding benefit of exceptions is their ability to signal error conditions in such a way that they cannot be ignored (Meyers 1996). Other approaches to handling errors create the possibility that an error condition can propagate through a code base undetected. Exceptions eliminate that possibility.

## Throw an exception only for conditions that are truly exceptional

Exceptions should be reserved for conditions that are truly exceptional—in other words, for conditions that cannot be addressed by other coding practices. Exceptions are used in similar circumstances to assertions—for events that are not just infrequent but for events that should never occur.

Exceptions represent a tradeoff between a powerful way to handle unexpected conditions on the one hand and increased complexity on the other. Exceptions weaken encapsulation by requiring the code that calls a routine to know which exceptions might be thrown inside the code that’s called. That increases code complexity, which works against what Chapter 5, “Design in Construction,” refers to as Software’s Primary Technical Imperative: Managing Complexity.

## Don’t use an exception to pass the buck

If an error condition can be handled locally, handle it locally. Don’t throw an uncaught exception in a section of code if you can handle the error locally.

## Avoid throwing exceptions in constructors and destructors unless you catch them in the same place

The rules for how exceptions are processed become very complicated very quickly when exceptions are thrown in constructors and destructors. In C++, for example, destructors aren’t called unless an object is fully constructed, which means if code within a constructor throws an exception, the destructor won’t be called, thereby setting up a possible resource leak (Meyers 1996, Stroustrup 1997). Similarly complicated rules apply to exceptions within destructors.

Language lawyers might say that remembering rules like these is “trivial,” but programmers who are mere mortals will have trouble remembering them. It’s better programming practice simply to avoid the extra complexity such code creates by not writing that kind of code in the first place.

Cross-Reference For more on maintaining consistent interface abstractions, see "Good Abstraction" in Section 6.2.

## Throw exceptions at the right level of abstraction

A routine should present a consistent abstraction in its interface, and so should a class. The exceptions thrown are part of the routine interface, just like specific data types are.
