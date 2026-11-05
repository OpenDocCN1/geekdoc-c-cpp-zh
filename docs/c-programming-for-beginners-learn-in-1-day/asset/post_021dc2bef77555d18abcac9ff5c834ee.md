
## Streams – Reading and Writing to files

In C# file operations, normally streams are used to read and write to files. A stream is an additional layer created between an application and a file. The stream is used to ensure smooth read and write operations to the file.

Streams are normally used when reading data from large files. By using streams, the data from large files is broken down into small chunks and sent to the stream. These chunks of data can then be read from the application.

The reason for breaking it down into small chunks is because of the performance impact of reading a big file at one shot. If you were to read the data from say, a 100 MB file at one shot, your application could just hang and become unstable. The best approach is then to use streams to break the file down into manageable chunks.

So when a write operation is carried out on the file, the data to be written is first written to the stream. From the stream, the data is then written to the file. The same goes for the read operation. In the read operation, data is first transferred from the file to the stream. The data is then read from the application via the stream. Let’s look at an example of how we can read and write using streams.

For our example, we will assume that we have a file in the D drive called Example.txt. The file will be a simple text file and have 2 lines as shown below.

```
Guru99 - .Net
Guru99 - C#
```

For our example, we will create a simple Console application and work with File streams.

### 1. Stream Reader

The stream reader is used to read data from a file using streams. The data from the file is first read into the stream. Thereafter the application reads the data from the stream.

Let’s look at an example of how we can use streams for reading data from a file. Enter the below code in the program.cs file.

```
string path = @"D:\Example.txt";

using (StreamReader sr = File.OpenText(path)){
    string s = "";
    while ((s = sr.ReadLine()) != null)
    {
        Console.WriteLine(s);
    }
}
Console.ReadKey();
```

- Defining the stream reader
- Defining temporary string
- Reading each line of the stream

### Code Explanation:

- 1. First, we are declaring a stream reader object. The stream reader object is used in C# to define a stream from the file to the application. The data will be pushed from the file to the stream whenever data is read from the file. The File.OpenText is used to open the file “Example.txt” in read-only mode. The handler to the file is then sent to the stream reader object.
- 2. Next, we are defining a temporary variable ‘s’ which will be used to read all the data from the file.
- 3. We then use the stream reader method ReadLine to read each line from the stream buffer. When we perform this operation, each line will be first transferred from the file to the buffer. Then the string line will be transferred from the buffer to the variable ‘s’. We then write the contents of the string ‘s’ to the console.

When the above code is set, and the project is run using Visual Studio, you will get the below output.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_162_0.png)

From the output, you can clearly see that the Stream Reader read both the lines from the file. Finally, the lines of the string read from the stream were sent to the Console.

### 2. Stream Writer

The stream writer is used to write data to a file using streams. The data from the application is first written into the stream. Thereafter the stream writes the data to the file. Let’s look at an example of how we can use streams for writing data to a file. Enter the below code in the program.cs file.

![](img/8115a2172ef67838d7fe1933fc517c4d_163_0.png)

### Code Explanation:

- 1. First, we are declaring a stream writer object. The stream writer object is used in C# to define a stream. The stream is then used to write data from the application to the file. The data will be pushed from the application to the stream whenever data needs to be written. The File.AppendText command is used to open the file “Example.txt” in an append mode. The handler to the file is then sent to the stream writer object.
- 2. We are using the stream writer method WriteLine to write the line “Guru99 – ASP.Net” to the stream. From the stream, the line will then be written to the file.
- 3. We then close the stream writer after writing to the file. It’s normally a good practice to close file handlers when the file is no longer required for writing purposes.
- 4. Finally, we are reading the contents of the file again and writing it to the console log. This is to check as to whether the line was really written to the file.

When the above code is set, and the project is run using Visual Studio, you will get the below output.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_164_0.png)

From the output, you can see that the line “Guru99 – ASP.Net” was added to the file successfully. All the 3 lines of text can be clearly seen in the console.

## C# Serialization

The concept of Serialization and deserialization is used whenever data pertaining to objects have to be sent from one application to another. Serialization is used to export application data into a file. The destination application then uses deserialization to extract the data from the application for further use.

Serialization is a concept in which C# class objects are written or serialized to files. Let’s say you had a C# class called Tutorial. And the class has 2 properties of ID and Tutorial's name.

Serializing can be used to directly write the data properties of the Tutorial class to a file. Deserialization is used to read the data from the file and construct the Tutorial object again.

Let’s look at an example of how we can achieve this.

In our example, we are going to perform the below high-level steps in the code.

- 1. Create a class called Tutorial which has 2 properties, namely ID and Name.
- 2. We will then create an object from the class and assign a value of “1” to the ID property and a value of “.Net” to the name property.
- 3. We will then use serialization to serialize the above object to a file called Example.txt.
- 4. Finally, we will use deserialization to deserialize the object from the file and display the values in the Console.

Enter the below code in the program.cs file of the console application.

### Step 1) The first step is to add the class which will be used for serialization

![](img/8115a2172ef67838d7fe1933fc517c4d_165_0.png)

### Code Explanation:

- 1. The class which needs to be serialized needs to have the [Serializable] attribute. This is a keyword in C#. This keyword is then attached to the Tutorial class. If you don’t mention this attribute, you will get an error when you try to serialize the class.
- 2. Next is the definition of the class which will be serialized. Here we are defining a class called “Tutorial” and providing 2 properties, one is “ID” and the other is “Name.”

### Step 2) In this step, first we will create the object of the Tutorial class and serialize it to the file called Example.txt

![](img/8115a2172ef67838d7fe1933fc517c4d_166_0.png)

### Code Explanation:

- 1. First, we create an object of the Tutorial class. We then assign the value of “1” to ID and “.net” to the name property.
- 2. We then use the formatter class which is used to serialize or convert the object to a binary format. The data in the file in serialization is done in binary format. Next, we create a file stream object. The file stream object is used to open the file Example.txt for writing purposes. The keywords FileMode.Create and FileAccess.Write are used to specifically mention that the file should be opened for writing purposes.
- 3. Finally, we use the Serialize method to transfer the binary data to the file. We then close the stream, since the write operation is complete.

### Step 3) Finally, to ensure that the data is present in the file, we use deserialization to deserialize the object from the file.
