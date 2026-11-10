# 14.2.2 Combining Declaration, Definition and Initialization

The preceding definitions created the variables `disk1` and `disk2` without initializing them. It is possible to combine declaration and definition by adding the variable name after the closing curly brace (Form 1). It is also possible to simultaneously initialize the variable (Form 2):

| Form 1 | Form 2 |
|---|---|
| `struct music cd {`<br>`  char title[30];`<br>`  short qty;`<br>`  float price;`<br>`} disk1;` | `struct music cd {`<br>`  char title[30];`<br>`  short qty;`<br>`  float price;`<br>`} disk2 = {"Beethoven", 3, 12.5};` |

For an initialized structure, the variable name is followed by an `=` and a list of comma-delimited values enclosed by curly braces. These initializers obviously must be provided in the right order. In Form 2, `"Beethoven"` is assigned to `title` and `3` to `qty`.

You can create multiple variables and initialize them at the same time, as shown in the following snippets which represent the last line of declaration:

```
    } disk1, disk2, disk3;
    } disk1 = {"Beethoven", 3, 12.5}, disk2 = {"Mahler", 4, 8.75};
```

Like with arrays, you can partially initialize a structure. If you initialize only `title`, the remaining members, `qty` and `price`, are automatically assigned zeroes.

By default, uninitialized structures have junk values unless they are global. A structure defined before `main` is a global variable, which means that the members are automatically initialized to zero or NULL.

# 14.2.3 Declaring without Structure Tag

If declaration and definition are combined, the structure tag can be omitted. This is usually done when no more structure variables of that type require to be defined later in the program. The following statement has the tag missing:

```
    struct {
      char title[30];
      short qty;
      float price;
    } disk4 = {"Borodin", 5}, disk5 = {"Schubert"};

    No tag specified
```

You can’t subsequently create any more variables of this type. Here, both `disk4` and `disk5` are partially initialized, which means that `disk4.price`, `disk5.qty` and `disk5.price` are automatically initialized to zeroes.

> Note: The structure tag is necessary when a structure is declared and defined at two separate places.