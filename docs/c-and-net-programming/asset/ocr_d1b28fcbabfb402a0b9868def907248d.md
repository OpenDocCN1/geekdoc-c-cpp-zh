# Example

```
num => num >10
```

The first part, before the ‘=>’ symbol, is refereed as the input parameter. It is not required to define it previously. It is dynamic. The type of ‘num’ variable is decided based on the operation performed on it.

# 12.5 Expression Trees

# Concept

Expression trees enable expressions to be represented as data structures.

# Explanation

Each node in an expression tree is an expression. For example, an expression tree can be used to represent mathematical formula x < y where x, < and y will be represented as an expression and arranged in the tree like structure.

They are used extensively by LINQ providers to translate query expressions into code that is meaningful in some other context, such as a SQL database.

Expression tree is an in-memory representation of a lambda expression. It holds the actual elements of the query, not the result of the query.

The expression tree makes the structure of the lambda expression transparent and explicit. One can interact with the data in the expression tree just as one can with any other data structure.

# Example

# Consider expression in C#,

```
Expression<Func<Customer, bool>> isNonSeniorCitizenExpr = s =>
s.age > 19 && s.age < 65;
```

# Expression Tree in C# for above expression is as follows,

```
Expression.Lambda<Func<Customer, bool>>(Expression.AndAlso
(Expression.GreaterThan(Expression.Property(pe, "Age"), Expression.Constant(19, typeof(int))),
Expression.LessThan(Expression.Property(pe, "Age"), Expression.Constant(65, typeof(int)))),
new[] { pe });
```

# 3.6 Checked and Unchecked Operator

# Concept

C# provides the checked and Unchecked operators that are two new features in C# for developers. These two operators force the CLR (Common Language Runtime) to handle