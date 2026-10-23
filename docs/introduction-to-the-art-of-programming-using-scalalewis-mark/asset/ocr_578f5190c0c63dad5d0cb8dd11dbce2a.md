edit the values in cells. To work with the Table in code, we need to have a name to refer to the Table by. We can get this by modifying the code slightly so we have a variable called `table`.

```
val table = new Table(data,colHeads)
...
  contents = new ScrollPane(table)
...
```

To get values out of the table, simply index it with a row and a column. So if you were to do the following line in the REPL you would see the value of the top-left cell.

```
println(table(0,0))
```

If you did this immediately after creating the table you would get back the value 1. However, if you edit that cell in the Table manually then print it, you will see the modified value. You can modify values in the Table in the same manner. Simply do an assignment into the Table indexed by row and column. Try this by doing the following in the REPL.

```
table(1,1) = "New text"
```

You will see that the value in cell (1,1) of the Table is updated graphically to reflect the change. This approach can only be used to modify cells within the normal bounds of the Table. If you go beyond the size set when you first created the Table you will get an error. If you try entering `table(0,0)` into the REPL you will get back a result with the type Any. This can be a bit of a problem because there are not many things that you can do with the Any type. For example, you might try doing the following.

```
table(0,0)+table(1,0)
```

Addition like this would work just fine for any numeric type or the String type as all of those types have the method `+` defined for them. However, if you try to do this you would get the following error message.

```
<console>:12: error: type mismatch;
 found   : Any
 required: String
        table(0,0)+table(0,0)
                    ^
```

That is because the type Any does not have a + method. This makes sense as there are some types that qualify as Any that you should not be able to use + with. To do anything with the values we get from the table we have to call methods that exist on Any. The challenge is that there are not very many of these. You can check for equality or inequality, doing operations associated with multithreading that will be discussed in chapter 21, check the actual type of the object, or convert the object to a String. The last two can provide the functionality that we want. We will focus on the last one because it uses only methods that we have seen before.

To convert any object to a String call the `toString` method. You can try the following to see how this works.

```
table(0,0).toString
```

Once you have done this you can use + to do String concatenation. If you want to do