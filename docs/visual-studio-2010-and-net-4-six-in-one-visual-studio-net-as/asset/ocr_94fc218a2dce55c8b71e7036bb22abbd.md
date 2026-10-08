programming model, many COM APIs utilize reference parameters. Contrary to references in C#, these are typically not meant to change a passed-in argument, but are simply another way of passing value parameters.

In Listing 24-1, a new Word document was created with the following code snippet:

```
var word = new Word.Application();
word.Visible = true;
object template = Type.Missing;
object newTemplate = Type.Missing;
object docType = Type.Missing;
object visible = Type.Missing;
word.Documents.Add(
  ref template,
  ref newTemplate,
  ref docType,
  ref visible);
```

This demonstrates very well that a C# programmer should have to create temporary variables for all ref parameters and pass them by reference. Type.Missing is immutable, so passing a reference to it is not a real benefit for the called method.

Instead, for COM methods, the C# 4.0 compiler will allow you to pass arguments by value to a method, and automatically generate temporary variables to hold the passed-in values. The subsequently discards them when the call returns. Listing 24-2 carries out the same task more intuitively:

```
var word = new Word.Application();
word.Visible = true;
word.Documents.Add();
```

In this way, the caller sees value semantics and not experience any side effects, but the called method still gets a reference.

# Indexed Properties

COM has a concept called parameterized properties that does not exist in C#. Until now, you had to use get_X() and set_X() methods to access the values of an indexed property x. For example, you could set the top-left cell of an Excel sheet as follows:

```
var excel = new Excel.Application();
excel.get_Range("A1").SetValue(Type.Missing, "Name");
```

Earlier, without indexed properties support, you would have to use the ugly Value2 property, because otherwise would have to call get_Value() or set_Value():

```
var excel = new Excel.Application();
excel.get_Range("A1").Value2 = "Name";
```