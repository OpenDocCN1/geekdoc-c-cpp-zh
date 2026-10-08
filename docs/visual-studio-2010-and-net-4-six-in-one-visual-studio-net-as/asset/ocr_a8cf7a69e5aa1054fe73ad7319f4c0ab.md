In the concrete example of the C# programming language, the type system is the .NET Framework's Common Type System (CTS). It's pretty easy to define that x and y are equal if and only if typeof(X).Equals(typeof(Y)). It is also easy to imagine that x is greater than y if they are on the same inheritance, and x is closer to the root of the chain than y.

To define the complete ordering among the types of CTS (including unrelatedness) is a complex task, — just think about generic types. The remaining discussions in this chapter focus on the practical side of variance, and its implementation in C# 4.0.

> If you want to dive into this topic deeper and obtain more authentic information on variance, Eric Lippert's blog, starting with this: http://blogs.msdn.com/erlicippert/archive/2007/10/16/covariance-and-variance-in-c-part-one.aspx.

# Variance in C# 4.0

Right now, C# implements only a subset of behavior that theoretically could be achieved by covariance and contravariance. However, the language designers achieved with this new variance is significant and really practical. The current variance implementation can be characterized with the following points:

+   * For non-generic types, nothing has been changed from the previous version of C# by means of variance.
* The way of providing variance for generic types is by marking types of a generic type as variant. Because a restriction in the CLR, type parameters can be declared only on generic interface and delegate types.
* Variance only applies when there is a reference conversion between type arguments. For example, variance applies for IEnumerable<string> and IEnumerable<object> because there is a reference conversion between string and object. However, the conversion from int to object is a boxing conversion, and so variance does not apply for IEnumerable<int> and IEnumerable<object>.
* Variance is not automatic. The compiler will not infer whether a type parameter is covariant or contravariant. Developers must explicitly declare their intention.

# Covariance

Following is an example of covariance:

```
IList<string> strings = new List<string>();
IEnumerable<object> objects = strings;
```

This works in C# 4.0. The compiler accepts it and generates proper code for executing the previous declarations. The key for this behavior is that IEnumerable<T> and IEnumerator<T> interfaces are declared with a variant type parameter T: