# Item 42: Understand How to Make Use of the Expression API 255

Expressions look like code. And, in many uses, expressions do compile down to delegates. However, you can ask for expressions in an Expression format. When you do that, you have an object that represents the code you want to execute. You can examine that expression, much like you can examine a class using the Reflection APIs. In the other direction, you can build an expression to create code at runtime. Once you create the expression tree you can compile and execute the expression. The possibilities are endless. After all, you are creating code at runtime. I’ll describe two common tasks where expressions can make your life much easier.

The first solves a common problem in communication frameworks. The typical workflow for using WCF, remoting, or Web services is to use some code generation tool to generate a client-side proxy for a particular service. It works, but it is a somewhat heavyweight solution. You’ll generate hundreds of lines of code. You’ll need to update the proxy whenever the server gets a new method, or changes parameter lists. Instead, suppose you could write something like this:

```
var client = new ClientProxy<IService>();
var result = client.CallInterface<string>(
server => server.DoWork(172));
```

Here, the ClientProxy<T> knows how to put each argument and method call on the wire. However, it doesn’t know anything about the service you’re actually accessing. Rather than relying on some out of band code generator, it will use expression trees and generics to figure out what method you called, and what parameters you used.

The CallInterface() method takes one parameter, which is an Expression<Func<T, TResult>>. The input parameter (of type T) represents an object that implements IService. TResult, of course, is whatever the particular method returns. The parameter is an expression, and you don’t even need an instance of an object that implements IService to write this code. The core algorithm is in the CallInterface() method.

```
public TResult CallInterface<TResult>(Expression<Func<T, TResult>> op)
{
	var exp = op.Body as MethodCallExpression;
	var methodName = exp.Method.Name;
	var methodInfo = exp.Method;
}
```