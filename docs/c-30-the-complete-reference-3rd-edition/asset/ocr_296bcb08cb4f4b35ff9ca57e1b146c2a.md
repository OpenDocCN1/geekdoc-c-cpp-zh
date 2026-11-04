```
// Now, read the data.
try {
    dataIn = new
        BinaryReader(new FileStream("testdata", FileMode.Open));
}
catch(IOException exc) {
    Console.WriteLine("Cannot Open File For Input");
    Console.WriteLine(exc.Message);
    return;
}

try {
    i = dataIn.ReadInt32();
    Console.WriteLine("Reading " + i);

    d = dataIn.ReadDouble();
    Console.WriteLine("Reading " + d);

    b = dataIn.ReadBoolean();
    Console.WriteLine("Reading " + b);

    d = dataIn.ReadDouble();
    Console.WriteLine("Reading " + d);

    str = dataIn.ReadString();
    Console.WriteLine("Reading " + str);
}
catch(IOException exc) {
    Console.WriteLine("Error Reading File");
    Console.WriteLine(exc.Message);
}

dataIn.Close();
}
```

The output from the program is shown here:

Writing 10
Writing 1023.56
Writing True
Writing 90.28
Writing This is a test

Reading 10
Reading 1023.56
Reading True
Reading 90.28
Reading This is a test

If you examine the testdata file produced by this program, you will find that it contains binary data, not human-readable text.

Here is a more practical example that shows how powerful binary I/O is. The following program implements a very simple inventory program. For each item in the inventory, the