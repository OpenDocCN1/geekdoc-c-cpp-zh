# Example 184 Input and Output: Eleven in One

This example illustrates out a human-readable text file: input and output of simple values with binary files; input and output of arrays with binary files; input and output of simple values with random access binary files; input and output using strings and string builders; to standard output and error output; and from standard input.

```
// Write numbers and words on file "f.txt" in human-readable form:
Writer tw = new StreamWriter(FileStream("f.txt", FileMode.Create));
tw.Write(4711); tw.Write(" "); tw.Write("cool"); tw.Close();
// Write simple values to a binary file "p.dat"
BinaryWriter bwr = new BinaryWriter(FileStream("p.dat", FileMode.Create));
bwr.Write(4711); bwr.Write("cool"); bwr.Close();
// Read simple values from a binary file "p.dat"
BinaryReader br = new BinaryReader(FileStream("p.dat", FileMode.Open));
Console.WriteLine(br.ReadInt32() + " + " + br.ReadChar() + " + " + br.ReadString());
n// Write an object or array to binary file "o.dat"
FileStream fs = new FileStream("o.dat", FileMode.Create);
BinaryFormatter bf = new BinaryFormatter();
bf.Serialize(fs, new int[] { 1, 2, 5, 11 }); fs.Close();
// Read objects or array from binary file "o.dat" in arbitrary order
FileStream fs = new FileStream("o.dat", FileMode.Open);
int ia = (int[])bf.Deserialize(fs);
Console.WriteLine(ia[0] + " (" + ia[1] + ", " + ia[2] + ", " + ia[3] + ", " + ia[4] + ");\ fs.Close();
// Read and write parts of file "raf.dat" in arbitrary order
FileStream fs = new FileStream("raf.dat", FileMode.OpenCreate, FileAccess.ReadWrite);
BinaryWriter bwr = new BinaryWriter(fs);
bwr.Write(34115); bwr.Write("SeekOrigin.Begin");
fs.Seek(0, SeekOrigin.Begin);
BinaryReader br = new BinaryReader(fs);
Console.WriteLine("1", + br.ReadDouble() + ", " + br.ReadInt32());
// Read as a string if it was a text file
TextWriter tw = new StreamWriter("abc");
Console.WriteLine("abc": " + (char)tr.Read() + " + (char)tr.Read() + " + " + (char)tr.Read());
// Write to a StringBuilder if it was a text file
TextWriter tw = new StreamWriter(sb);
tw.Write("d"); tw.Write("e"); tw.Write("f");
Console.WriteLine(tw.ToString());
// Write characters to standard output and error
Console.Out.WriteLine("std output"); Console.Error.WriteLine("std error");
// Read characters from standard input (the keyboard)
Console.Write("Type some characters and press Enter: ");
Reader in = Console.In;
String response = in.ReadLine();
Console.WriteLine("You typed: '"' + response);
// Read a character from standard input (the keyboard)
Console.Write("Type one character and press Enter: ");
char c = (char)Console.In.Read();
Console.WriteLine("First character of your input is: " + c);
```