+   - **A joinpoint** is any place in the code where an advice *could* be applied. In theory, a joinpoint could be almost anything instance variable, `for` loop, `if` statement, and so on. In practice, however, most commonly used join-points are classes, methods, and properties.
+   - **A pointcut** identifies a set of joinpoints where advice *should* be applied. For example, if you want to apply transaction advice to all the methods that are marked with `transaction` attribute, you would have to declare a pointcut that identifies those methods.
+   - **An aspect** groups advices and the pointcuts they apply to, which is in a way similar to how a class groups data and associated behavior together.

# AOP in .NET

Enough theory let's see how AOP can help us solve real-world problems that we face almost every day during development.

Examples in this section are built using the Spring.NET AOP implementation, so you will need to download and install the latest Spring.NET release in order to try them.

# Note

Please note that, as of this book's writing, the examples in this section are based on the planned implementation of the AOP support in Spring. NET. Visit this book's Web site (www.jnsk.se/adddp) for information about changes, or check the official Spring.NET documentation, which can be found at www.springframework.net.

# Modularizing Logging Code Using an Aspect

So let's see how we can leverage AOP to solve the problems associated with the previous logging code.

# Creating a Logging Advice

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