```
}

Console::WriteLine(L"\n\nPopping integers off the stack produces:");
while((item = stack->Pop()) != nullptr)
    Console::Write(L"{0,5}",item);

Console::WriteLine();
return 0;
}
```

The output from this example is:

```
The array of boxes have the following volumes:
Box usable volume is 24
Box usable volume is 20.4
Box usable volume is 120
Box usable volume is 102

Now pushing the boxes on the stack...
Popping the boxes off the stack presents them in reverse order:
Box usable volume is 102
Box usable volume is 120
Box usable volume is 20.4
Box usable volume is 24

Now pushing integers on to the stack:
    2     4     6     8    10    12

Popping integers off the stack produces:
   12    10     8     6     4     2
Press any key to continue . . .
```

# How It Works

You first create an array of handles to strings:

```
array<Box^>^ boxes = { gcnew Box(2.0, 3.0, 4.0),
                       gcnew GlassBox(2.0, 3.0, 4.0),
                       gcnew Box(4.0, 5.0, 6.0),
                       gcnew GlassBox(4.0, 5.0, 6.0)
                     };
```

Because Box and GlassBox are ref classes, you create the objects on the CLR heap using gcnew. The addresses of the objects initialize the elements of the boxes array.

You then create a Stack object and push the strings on to the stack:

```
Stack^ stack = gcnew Stack;        // Create the stack
for each(Box^ box in boxes)
    stack->Push(box);
```