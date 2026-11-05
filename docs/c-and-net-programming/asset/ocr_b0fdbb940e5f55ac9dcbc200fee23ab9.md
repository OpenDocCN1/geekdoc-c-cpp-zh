```
string Title; //class member

public Book(string title)
{
//referring to current instance
this.Title=title;//"this.title" refers to class member
}

//calling another constructor
public Book():this("Programming")//calls Book(string title) before Book()
{
}

//declaring an indexer
public int this[int cnt]
{
get{return Title[cnt];}
set{Title[cnt]=value;}
}
```

# 8.1.5 Indexer

# Concept

+   1. An **indexer** is a method implemented that allows an object to be indexed just like an array.

# Explanation

+   2. When an indexer is defined for a class, this class behaves similar to a **virtual array**. Now, the instance of this class can be accessed using the array access operator ([ ]).\n3. An indexer provides array-like syntax. It allows a type to be accessed the same way as an array. Properties such as indexers often access a backing store.\n4. Indexer modifier can be private, public, protected or internal.\n5. The return type of indexer can be any valid C# types.\n6. Indexers in C# must have at least one parameter, else the compiler will generate a compilation error.\n7. In an indexer, often a int parameter is accepted and it accesses a backing array. Values in indexer can be initialized with an initializer.\n8. Indexer can be overloaded that is there can be multiple indexer in the class.

# General syntax of Indexer

```
this [Parameter]
{
```