with another substring. Using Replace, the code to encode the text looks like this (code file StringSample/Program.cs):

```
string greetingText ="Hello from all the guys at Wrox Press.";
greetingText +="We do hope you enjoy this book as much as we" + "enjoyed writing it.";

WriteLine($"Not encoded:\n {greetingText}");

for(int i = 'z'; i>= 'a'; i--)
{
    char old1 = (char)i;
    char new1 = (char)(i+1);
    greetingText = greetingText.Replace(old1, new1);
}

for(int i = 'Z'; i>='A'; i--)
{
    char old1 = (char)i;
    char new1 = (char)(i+1);
    greetingText = greetingText.Replace(old1, new1);
}

WriteLine($"Encoded:\n {greetingText}");
```

> NOTE Simply, this code does not change Z to A or z to a. These letters are encoded to [ and {, respectively.

In this example, the Replace method works in a fairly intelligent way, to the extent that it won’t actually create a new string unless it actually makes changes to the old string. The original string contained 23 different lowercase characters and three different uppercase ones. The Replace method will therefore have allocated a new string 26 times in total, with each new string storing 103 characters. That means because of the encryption process, there will be string objects capable of storing a combined total of 2,678 characters now sitting on the heap waiting to be garbage collected! Clearly, if you use strings to do text processing extensively, your applications will run into severe performance problems.

To address this kind of issue, Microsoft supplies the System.Text.StringBuilder class. StringBuilder is not as powerful as String in terms of the number of methods it supports. The processing you can do on a StringBuilder is limited to substitutions and appending or removing text from strings. However, it works in a much more efficient way.

When you construct a string using the String class, just enough memory is allocated to hold the string object. The StringBuilder, however, normally allocates more memory than is actually needed. You, as a developer, have the option to indicate how much memory the StringBuilder should allocate; but if you do not, the amount defaults to a value that varies according to the size of the string with which the StringBuilder instance is initialized. The StringBuilder class has two