
# Chapter 21 Generic Collections: Functional Programming with LINQ/PLINQ

- The compiler converts LINQ queries into calls to extension methods—many of which have delegate parameters.

## Section 21.8.1 Declaring a Delegate

- A delegate is declared by preceding a method header with keyword delegate (placed after any access specifiers, such as public or private) and following the method header with a semi-colon.
- A delegate type declaration includes the method header only—the header describes a set of methods with specific parameters and a specific return type.

## Section 21.8.2 Declaring a Delegate Variable

- A delegate variable can hold a reference to any method with a matching signature.

## Section 21.8.3 Delegate Parameters

- The real power of delegates is in passing method references as arguments to methods.

## Section 21.8.4 Passing a Method Name Directly to a Delegate Parameter

- A method can be passed directly to a delegate parameter, rather than assigning it to a delegate variable.

## Section 21.9 Lambda Expressions

- Lambda expressions allow you to define simple, anonymous methods—that is, methods that do not have names and are defined where they are assigned to a delegate or delegate parameter.
- Working with lambda expressions can reduce the size of your code and the complexity of working with delegates.

## Section 21.9.1 Expression Lambdas

- A lambda expression begins with a parameter list and is followed by the => operator and an expression that represents the lambda's body.
- The value produced by the expression is implicitly returned by the lambda expression.
- An expression lambda has a single expression to the return type of the lambda operator.
- A lambda's return type is inferred from the return value or, in some cases, from a delegate's return type.

## Section 21.9.2 Assigning Lambdas to Delegate Variables

- A delegate can hold a reference to a lambda expression that has a signature that is compatible with the delegate type.
- A lambda expression is called via a variable that references it.

## Section 21.9.3 Explicitly Typed Lambda Parameters

- Lambda expressions are often used as arguments to methods with delegate-type parameters, rather than defining and referencing a separate method or defining a delegate variable that references a lambda.
- You can explicitly type a lambda expression's parameters.
- When specifying a lambda parameter's type and/or when a lambda has more than one parameter, you must enclose the parameter list in parentheses.

## Section 21.9.4 Statement Lambdas

- A statement lambda contains a statement block—one or more statements enclosed in braces ({}) to the right of the lambda operator.

## Section 21.10 Introduction to Functional Programming

## Section 21.11 Functional Programming with LINQ Method-Call Syntax and Lambdas

## Section 21.11.1 LINQ Extension Methods Min, Max, Sum and Average

- Class Enumerable (namespace System.Linq) defines the LINQ to Objects extension methods.

## Section 21.11.2 Aggregate Extension Method for Reduction Operations

- You can define your reductions with the Aggregate LINQ extension method.
- The version of Aggregate demonstrated in the chapter receives two arguments—a value that helps you reduce the reduction operation and a Func delegate (namespace System) representing a method that receives two arguments and returns a value and specifies how to reduce the arguments. For each element in the collection, Aggregate calls this lambda expression.
- On the first call to the lambda, Aggregate's first argument and the first element of the collection are passed. Subsequent call to the lambda uses the result of the previous call as the lambda's first argument and the next element of the collection as the second. This continues until all elements of the collection have been processed to reduce the collection to a single value.

## Section 21.11.3 The Extension Method for Filtering Operations

- Filter elements to produce a collection of results that match a condition—known as a predicate.
- LINQ extension method where receives its argument as a Func delegate for a method that receives one argument and returns a bool indicating whether a given element should be included in the collection returned by where.
- The Order method receives its argument as a Func delegate representing a method that receives one parameter (element in the collection) and returns a value that's used to order the results.
- Calls to where and Order used deferred execution—they aren't evaluated until you iterate over the results.

## Section 21.11.4 Select Extension Method for Mapping Operations

- Mapping transforms a collection's elements to new values, sometimes are of different types from the original elements.
- LINQ extension method Select receives its argument as a Func delegate for a method that receives one argument (element in the collection) and maps it to a new value (possibly of other type) that's included in the collection returned by Select.

## Section 21.12.1 PLINQ: Improving LINQ to Objects Performance with Multicore

- A concept called enables the operation system to run parts of an query concurrently.
- Though of all these tasks can make progress concurrently, they may do so by sharing one process core.
- With multicore processors, can one app's threads operate truly in parallel on separate cores.
- The operating system can allow one app's threads to operate truly in parallel on separate cores, possibly increasing the app's performance stability.
- Parallelizing algorithms and algorithms to handle multiple cores is difficult and highly risky, especially if they share data that can be modified by one or more of the tasks.
- Another benefit of functional programming is that you can ask the library to perform a task with parallel processing to advantage of multiple cores. This is the purpose of PLQ (Parallel LINQ)—an implementation of the LINQ to Objects extension methods that parallelizes the operations for increased performance.
- Class Enumerable provides static method Range to produce an IEnumerable<int> containing values in sequence. The first argument specifies the value in the range and the second specifies the number of values to produce.
- Extension method ToArray returns an array representation of an IEnumerable<T>'s contents. Class Enumerable also provides method ToList to obtain a List<T> rather than an array.
- DateTime's Now property gets the current time.

- DateTime method Subtract compute the difference between two DateTimes, which is returned as a TimeSpan.
- TimeSpan.TotalMilliseconds returns the number of milliseconds represented by the TimeSpan.
- To initiate parallel processing, invoke IParallel<T> extension method AsParallel(from class ParallelEnumerable), which returns a ParallelQuery<T>.
- An object that implements ParallelQuery<T> can be used with PLINQ to parallelize versions of the LINQ extension methods.
- Class Enumerable defines the ParallelQuery<T> (PLINQ) parallelized versions of LINQ to Objects extension methods as well as several PLINQ-specific extension methods.

## Section 21.13 (Optional) Covariance and Contravariance for Generic Types

- C supports covariance and contravariance of generic interface and delegate types.
- Assigning an array of a derived-class to an array variable of a base-class type is an example of covariance.
- Covariance works with several generic interfaces, including IEnumerable<T>.
- Using a cast to assign an array variable of a base-class type to an array variable of a derived-class type is an example of contravariance.
- SortedSet maintains a set of objects in sorted order--no duplicates are allowed.
- The objects in a SortedSet must be comparable to determine their sorting order. Objects are compared if their classes implement IComparable<T>.
- For classes that do not implement IComparable<T>, you can compare the objects using an object that implements IComparable<T> interface. This compare method compares its two arguments and returns 0 if they are equal, a negative integer if the first is less than the second, or a positive integer if the first object is greater than the second.
- Providing an IComparer for a base-class type where an IComparer for a derived-class type is expected because IComparer<T> supports covariance.
