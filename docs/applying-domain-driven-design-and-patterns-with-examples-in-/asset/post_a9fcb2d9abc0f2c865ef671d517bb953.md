
In large systems as it avoids the problematic situation where different components to be used in a system are tied to different locator implementations.

Another advantage of the Dependency Injection pattern, especially with Constructor Dependency Injection, is that all dependencies of an object are easily visible in code. Modern IDEs are capable of highlighting all usages of a service locator in a given class (by pressing Ctrl-Shift-F7), but even with a sophisticated IDE this is not as easy as looking at a constructor.

It is often stated that Dependency Injection couples the life cycle of the object A that has the dependencies with the life cycles of the objects B and C it depends on, because B and C must be created before A so that they can be injected. This is not a problem with the Service Locator pattern because the creation of B and C can be postponed until they are requested from the locator by A. Fortunately, the same can be achieved, if not as naturally, with the Dependency Injection pattern, as one usage of the Component Adaptors in PicoContainer shows. Instead of injecting an instance of the actual class, the container injects a proxy that only creates the real instance when it is first used and from then on forwards all method calls to it. This is completely transparent to the object that has the dependencies, but it effectively decouples their lifecycles.

## Summary

In this section, we looked at two issues that arise in the construction of any software system: the coupling of objects that depend on other objects and the managing of component instances. We first described how these issues can be addressed with the commonly used Factory, Registry, and Service Locator patterns. Realizing that these patterns have certain shortcomings, we discussed the Dependency Injection pattern, which addresses these issues in a novel way. This pattern, which is based on the Inversion of Control principle, provides better decoupling and scales well, from simple problems to very complex dependencies. It also improves testability, which is important for TDD, and allows domain models to be completely separated from infrastructure code, which makes it a useful tool for DDD.

As with almost any pattern, Dependency Injection is not a silver bullet and one cannot make the general recommendation to always replace the use of the Service Locator pattern with Dependency Injection. It is important to understand the differences and benefits of each pattern and use them appropriately. We have also seen that the Dependency Injection pattern has several flavors that provide trade-offs. Fortunately, choosing a certain flavor does not affect testability, which is important for development, and the containers that are used at runtime generally support all main variants. We can therefore choose, or even mix, different flavors as required.

The most important consideration when designing systems is to separate concerns, in this case configuration and usage of components, and then choose the most suitable design pattern from a rich catalogue.

Thanks, Erik!

I just want to stress once more what Erik ended with. You can think about Dependency Injection as what Martin Fowler talks about in his DSL article [Fowler LW] when he says that development can be thought of as creating good abstractions and then configuring them. Dependency Injection is one approach to taking care of part of the configuration.

I had to bite my tongue not to say "configuration aspect" in the previous sentence. You wouldn't have forgiven me for providing such a weak thread to the next subject, right? As a matter of fact,

one-liners had to be broken into result assignment and its return, just so the result could be printed in the logging code.

- If you had to remove logging code at some point, you would be faced with a daunting task of manually removing or commenting out all the logging code from your classes.
- If you decided that you want to log the full class name, including namespace, you would have to find all the methods that contain logging code and add missing namespace information by hand.
- The same applies if you decide that you want to log exceptions such as overflow and division by zero when they occur—you'd have to add a try/catch block and a statement that would log exceptions in many, many places throughout your code base.

Of course, one could argue that if you used a sophisticated logging solution, such as Log4Net [Log4Net] or Enterprise Library Logging Application Block [Enterprise Library Logging], instead of plain `Console.Out.WriteLine` statements, you could turn logging off by simply changing the configuration setting, without the need to touch any of your classes.

While that is entirely true, it really misses the point in this case. Your core logic would still be intermingled with ancillary logging code, and you would still have to edit many methods by hand if you wanted to make any changes to the logging logic. Moreover, if we change our example from logging to security policy enforcement or transactions, you won't be able to turn it on or off so easily either.

What AOP promises to do for you is to allow you to separate crosscutting code, such as logging or security, into aspects and to apply those aspects easily to all the classes and methods that need them. Of course, there is a lot more to AOP than this. It also allows you to separate business rules from the core logic and to change your existing objects by adding both state and behavior to them. We'll see examples of this in the following sections.

What is important to understand is that AOP is not a replacement for OOP—it is simply an extension to it that allows you to go to places that are difficult to reach with OOP alone. Good object-oriented principles and practices still apply. Actually, it is probably even more important than ever before to have a solid OO design in place, as it will make application of aspects much easier.

## AOP Terminology Defined

Before we dig deeper and show you examples of AOP in action, it is important to understand basic AOP terminology, which is not as difficult as it first seems. So I offer some definitions for the following terms:

- An **advice** is a piece of code that you want to encapsulate and reuse. For example, logging code would be implemented as an advice and applied wherever you need it. There are several types of advice, such as *before*, *after*, and *around* advice.
- An **introduction** is a somewhat special type of advice that only applies to classes. Introductions allow you to introduce new members into existing classes, both state and behavior, and could be used to achieve the benefits of multiple inheritance in languages that do not support it, without its tradeoffs. (Introduction is called *mixin* in some languages.)
- **A joinpoint** is any place in the code where an advice *could* be applied. In theory, a joinpoint could be almost anything instance variable, `for` loop, `if` statement, and so on. In practice, however, most commonly used join-points are classes, methods, and properties.
- **A pointcut** identifies a set of joinpoints where advice *should* be applied. For example, if you want to apply transaction advice to all the methods that are marked with `transaction` attribute, you would have to declare a pointcut that identifies those methods.
- **An aspect** groups advices and the pointcuts they apply to, which is in a way similar to how a class groups data and associated behavior together.

## AOP in .NET

Enough theory let's see how AOP can help us solve real-world problems that we face almost every day during development.

Examples in this section are built using the Spring.NET AOP implementation, so you will need to download and install the latest Spring.NET release in order to try them.

## Note

Please note that, as of this book's writing, the examples in this section are based on the planned implementation of the AOP support in Spring.NET. Visit this book's Web site (www.jnsk.se/adddp) for information about changes, or check the official Spring.NET documentation, which can be found at www.springframework.net.

## Modularizing Logging Code Using an Aspect

So let's see how we can leverage AOP to solve the problems associated with the previous logging code.

## Creating a Logging Advice

The first thing we need to do is create an advice that will encapsulate logging code:

```
using System;
using System.Text;
using AopAlliance.Intercept;

namespace LoggingAspectDemo
{
    public class MethodInvocationLoggingAdvice
        : IMethodInterceptor
    {
```
