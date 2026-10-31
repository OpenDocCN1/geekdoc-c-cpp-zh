
要么直接实现行为，要么让它们继承自某个实现了核心锁定和解锁功能的基类。

第一种解决方案很糟糕，因为它会导致大量重复代码。第二种方案只有在需要锁定行为的类属于同一个类层次结构且所有这些类都需要支持锁定时才可行。如果它们属于不同的层次结构，或者你不想将锁定行为引入到所有这些类中，那么就又回到了原点。

更好的方法是利用AOP特性，以声明方式仅为需要锁定的类添加锁定支持。通过结合使用引入（introduction）和前置通知（before advice），可以轻松实现这一点。

## 实现锁定引入

这里的第一步是创建一个引入，用于向被通知的类添加状态和行为。为此，我们需要定义希望引入的接口。

```csharp
namespace LockableAspectDemo
{
    public interface ILockable
    {
        void Lock();
        void Unlock();
        bool IsLocked { get; }
    }
}
```

下一步是创建一个实现该接口的引入类。在本例中，我们假设正在编写一个 ASP.NET Web 应用程序，并将使用 HttpContext.Current.Session.SessionID 作为用于锁定的会话 ID。

```csharp
using AopAlliance.Aop;

namespace LockableAspectDemo
{
    public class LockableIntroduction : ILockable, IAdvice
    {
        private bool isLocked;
        private string sessionId;

        public void Lock()
        {
            isLocked = true;
            sessionId = HttpContext.Current.Session.SessionID;
        }

        public void Unlock()
        {
            isLocked = false;
            sessionId = null;
        }

        public bool IsLocked
        {
            get
            {
                return isLocked && sessionId
                    != HttpContext.Current.Session.SessionID;
            }
        }
    }
}
```

到目前为止，我们已经创建了想要使用的引入。现在需要创建一个通知，用于强制执行该引入所实现的锁定。

## 实现锁定强制通知

在特定情况下，我们不需要像日志示例中使用的那样完整的*环绕通知*。我们的通知所需要做的只是检查目标对象是否被锁定，如果是，则抛出异常。

为此，我们可以使用一种稍微简单的*前置通知*，它不需要我们调用 `MethodInvocation.Proceed()`：

```csharp
using System;
using System.Reflection;
using Spring.Aop;

namespace LockableAspectDemo
{
    public class LockEnforcerAdvice : IMethodBeforeAdvice
    {
        public void Before(MethodBase method, object[] args,
            object target)
        {
            ILockable lockable = target as ILockable;
            if (lockable != null && lockable.IsLocked)
            {
                throw new LockViolationException
                    ("Attempted to modify locked object.", target);
            }
        }
    }
}
```

## 将锁定切面应用于领域对象

有多个原因使得这个类适合基于代理的AOP。首先，属性是通过私有字段与属性getter和setter的组合实现的。如果你改用公有字段，AOP代理就不可能拦截属性访问。

其次，所有属性和方法都被声明为虚拟的。这允许Spring.NET通过继承`Account`类并注入拦截代码来创建动态代理。如果方法是final的，`Account`类就必须实现一个接口才能通过组合代理进行代理。如果既没有接口也没有虚拟方法，就不可能为`Account`类创建代理并对其应用AOP通知。

最后需要注意的一点是`StateModifier`特性的使用。我们定义这个特性主要是为了展示如何基于特性应用通知，但这也是使用特性非常有意义的一个案例。它提供了额外的元数据，使哪些方法修改对象状态变得一目了然。

我们本也可以在属性setter前面使用`StateModifier`特性，但在我看来这有些多余。此外，在属性的情况下省略`StateModifier`，让我们有机会向你展示如何定义复合切入点。

虽然可以仅使用代码方式来配置锁定切面，但这种方式有些繁琐，因此在这种情况下我们只展示声明式方法。

```xml
<aop:aspect name="LockEnforcementAspect">
    <aop:pointcut name="StateModifiers"
        expression="class(Account+)
        and (setter(*) or attribute(StateModifier))"/>
    <aop:advice type="LockableAspectDemo.LockableIntroduction"
        pointcut="class(Account+)"/>
    <aop:advice type="LockableAspectDemo.LockEnforcerAdvice"
        pointcut-ref="StateModifiers"/>
</aop:aspect>
```

声明中的大部分内容应该不言自明。值得注意的地方有：

- 切入点定义中类名后面的加号指定切入点应匹配指定类及其派生类。
- 表达式`"setter(*)"`用于匹配所有属性setter，无论其类型和名称如何。
- 表达式`"attribute(StateModifier)"`用于匹配所有标记了`StateModifier`特性的成员。

最后，我们需要创建一个客户端，它将利用引入的`ILockable`接口，就像该接口直接由`Account`类实现一样。

```csharp
using LockableAspectDemo.Domain;

namespace LockableAspectDemo.Services
{
    public class AccountManager
    {
        public void TransferFunds(Account from, Account to,
            double amount)
        {
            ILockable acctFrom = from as ILockable;
            ILockable acctTo = to as ILockable;

            try
            {
                acctFrom.Lock();
                acctTo.Lock();

                from.Withdraw(amount);
                to.Deposit(amount);
            }
            finally
            {
                acctFrom.Unlock();
                acctTo.Unlock();
            }
        }
    }
}
```

正如你所看到的，通过使用AOP，我们可以真正地模块化对象锁定功能，并在适当的地方应用它，而不存在纯OOP方法的缺点。

## 注意

尽管前面的示例在技术上与使用`lock`语句来同步多个线程对`acctFrom`和`acctTo`的访问没有区别，但两者在语义上存在很大差异。使用`ILockable`，我们可以在多个HTTP请求期间保持锁定，而不仅仅是单个请求。

## 将业务规则迁移到切面

本节要展示的最后一个示例演示了一种更为高级的AOP用法。我们不建议你通过将所有业务规则迁移到切面来开始尝试AOP。将AOP引入到你的项目中的最好方式可能是让它逐步处理明显的横切关注点，例如日志记录、安全性和事务。然而，我们认为重要的是你要理解它的全部潜力，以便在更加熟悉它之后能够有效地应用它。

每个业务应用程序都有各种业务规则，这些规则通常嵌入在应用程序逻辑中。虽然这对于大多数规则和大多数应用程序来说效果不错，但它使应用程序的灵活性低于实际需求，并且当业务规则发生变化时通常需要修改代码。通过将一些业务规则迁移到切面，你可以使应用程序更容易定制。与前面的示例不同，消除代码重复通常不是你将业务规则迁移到切面的主要原因——在这种情况下，主要驱动力是提高应用程序的灵活性。

最好的候选者是那些导致核心逻辑之外还要实现次要逻辑的规则。例如，前面示例中`Account.Withdraw()`方法的核心逻辑是减少账户余额。次要逻辑可能是强制执行最低余额要求，或者当余额低于某个金额时向账户持有人发送电子邮件提醒。

让我们看看，如果我们同时添加最低余额强制和余额提醒，`Account`类会是什么样子。

```csharp
using System;

namespace BusinessRulesDemo.Domain
{
    public class Account
    {
        private AccountHolder accountHolder;
        private string name;
        private double balance;
        private double minimumBalance;
        private double alertBalance;

        // Spring.NET IoC injected collaborators
        private INotificationSender notificationSender;

        public Account() { }

        public Account(string name, double balance)
        {
            Name = name;
            Balance = balance;
        }

        public virtual Person AccountHolder
        {
            get { return accountHolder; }
            set { accountHolder = value; }
        }

        public virtual string Name
        {
            get { return name; }
            set { name = value; }
        }

        public virtual double Balance
        {
            get { return balance; }
```
