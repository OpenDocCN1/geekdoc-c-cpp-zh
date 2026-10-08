```
double define_name(string var, double val)
{
    // add {var,val} to var_table
    if (is_declared(var)) error(var, "declared twice");
    var_table.push_back (Variable{var,val});
    return val;
}
```

Adding a new **Variable** to a **vector<Variable>** is easy; that’s what **vector’s push_back()** member function does:

```
var_table.push_back (Variable{var,val});
```

The **Variable(var,val)** makes the appropriate **Variable** and **push_back()**, then adds that **Variable** to the end of **var_table**. Given that, and assuming that we can handle **let** and **name** tokens, **declaration()** is straightforward to write:

```
double declaration()
{
    // assume we have seen "let"
    // handle: name = expression
    // declare a variable called "name" with the initial value "expression"
    Token t = ts.get();
    if (t.kind !=name) error ("name expected in declaration");
    string var_name = t.name;

    Token t2 = ts.get();
    if ((t2.kind !='=')) error("= missing in declaration of ", var_name);

    double d = expression();
    define_name(var_name,d);
    return d;
}
```

Note that we returned the value stored in the new variable. That’s useful when the initializing expression is nontrivial. For example:

```
let v = d/(t2-t1);
```

This declaration will define **v** and also print its value. Additionally, printing the value of a declared variable simplifies the code in **calculate()** because every **statement()** returns a value. General rules tend to keep code simple, whereas special cases tend to lead to complications.