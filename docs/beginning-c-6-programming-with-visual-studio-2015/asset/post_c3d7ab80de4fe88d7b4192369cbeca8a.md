
Alternatively, you can use literal values for initial assignment. Here, you use nested blocks of curly braces, separated by commas:

```csharp
double[,] hillHeight = { { 1, 2, 3, 4 }, { 2, 3, 4, 5 }, { 3, 4, 5, 6 } };
```

This array has the same dimensions as the previous one—that is, three rows and four columns. By providing literal values, these dimensions are defined implicitly.

To access individual elements of a multidimensional array, you simply specify the indices separated by commas:

```csharp
hillHeight[2,1]
```

You can then manipulate this element just as you can other elements. This expression will access the second element of the third nested array as defined previously (the value will be 4). Remember that you start counting from 0 and that the first number is the nested array. In other words, the first number specifies the pair of curly braces, and the second number specifies the element within that pair of braces. You can represent this array visually, as shown in Figure 5-10.

![](img/cf72ea860016d2d680fc085fc06f265a_124_0.png)

FIGURE 5-10

The `foreach` loop gives you access to all elements in a multidimensional way, just as with single-dimensional arrays:

```csharp
double[,] hillHeight = { { 1, 2, 3, 4 }, { 2, 3, 4, 5 }, { 3, 4, 5, 6 } };
foreach (double height in hillHeight)
{
    WriteLine("{0}", height);
}
```

The order in which the elements are output is the same as the order used to assign literal values. This sequence is as follows (the element identifiers are shown here rather than the actual values):

```text
hillHeight[0,0]
hillHeight[0,1]
hillHeight[0,2]
```

```csharp
new int[] { 1, 3 },
new int[] { 1, 2, 4 },
new int[] { 1, 5 },
new int[] { 1, 2, 3, 6 },
new int[] { 1, 7 },
new int[] { 1, 2, 4, 8 },
new int[] { 1, 3, 9 },
new int[] { 1, 2, 5, 10 } );
```

The following code will fail:

```csharp
foreach (int divisor in divisorsTo10)
{
    WriteLine(divisor);
}
```

The failure occurs because the array `divisorsTo10` contains `int[]` elements, not `int` elements. Instead, you have to loop through every sub-array, as well as through the array itself:

```csharp
foreach (int[] divisorsOfInt in divisorsTo10)
{
    foreach (int divisor in divisorsOfInt)
    {
        WriteLine(divisor);
    }
}
```

As you can see, the syntax for using jagged arrays can quickly become complex! In most cases, it is easier to use rectangular arrays or a simpler storage method. Nonetheless, there may well be situations in which you are forced to use this method, and a working knowledge can't hurt. An example of this happens when working with XML documents where some elements have sub-children and others do not.

## STRING MANIPULATION

Your use of strings so far has consisted of writing strings to the console, reading strings from the console, and concatenating strings using the `+` operator. In the course of programming more interesting applications, you will discover that manipulating strings is something that you end up doing a lot. Therefore, it is worth spending a few pages looking at some of the more common string-manipulation techniques available in C#.

To start with, a string-type variable can be treated as a read-only array of `char` variables. This means that you can access individual characters using syntax like the following:

```csharp
string myString = "A string";
char myChar = myString[1];
```

However, you can't assign individual characters this way. To get a `char` array that you can write to, you can use the following code. This uses the `ToCharArray()` command of the array variable:

```csharp
string myString = "A string";
char[] myChars = myString.ToCharArray();
```

## Small Object Detection

Small object detection is a challenging problem in computer vision, where objects occupy a tiny region in the image, often less than 32 × 32 pixels. Traditional detectors struggle with such objects due to limited information and context.

## Key Challenges

- Low resolution and tiny size
- Limited context and semantic information
- Imbalance between foreground and background
- Difficulty in feature extraction and localization

Recent advancements focus on feature pyramids, multi-scale training, and context augmentation to alleviate these issues.

The preceding code is also able to detect strings like this:

```text
" YES"
"Yes "
```

You can also use these commands to remove any other characters by specifying them in a `char` array, for example:

```csharp
char[] trimChars = { 't', 'e', 's' };
string userResponse = ReadLine();
userResponse = userResponse.ToLower();
userResponse = userResponse.Trim(trimChars);
if (userResponse == "y")
{
    // Act on response.
}
```

This eliminates any occurrences of spaces, as well as the letters `"e"` and `"s"` from the beginning or end of your string. Providing there aren't any other characters in the string, this will result in the detection of strings such as:

```text
"Yeeeees"
" y"
```

and so on.

You can also use the `<string>.TrimStart()` and `<string>.TrimEnd()` commands, which will trim spaces from the beginning and end of a string, respectively. These can also have `char` arrays specified.

You can use two other string commands to manipulate the spacing of strings: `<string>.PadLeft()` and `<string>.PadRight()`. They enable you to add spaces to the left or right of a string to force it to the desired length. You use them as follows:

```csharp
<string>.PadX(<desiredLength>);
```

The following code obtains the substrings you get when the string is split at each space—that is, you get an array of individual words:

```csharp
string[] myWords;
myWords = myString.Split(separator);
```

Next, you loop through the words in this array using `foreach` and write each one to the console:

```csharp
foreach (string word in myWords)
{
    WriteLine($"{word}");
}
```

> **NOTE** Each word obtained has no spaces, either embedded in the word or at either end. The separators are removed when you use `Split()`.

## EXERCISES

### 5.1 Which of the following conversions can't be performed implicitly?

- a. `int` to `short`
- b. `short` to `int`
- c. `bool` to `string`
- d. `byte` to `float`

### 5.2 Show the code for a color enumeration based on the `short` type containing the colors of the rainbow plus black and white. Can this enumeration be based on the `byte` type?

### 5.3 Will the following code compile? Why or why not?

```csharp
string[] blah = new string[5]
blah[5] = 5th string.
```

### 5.4 Write a console application that accepts a string from the user and outputs a string with the characters in reverse order.

### 5.5 Write a console application that accepts a string and replaces all occurrences of the string `no` with `yes`.

### 5.6 Write a console application that places double quotes around each word in a string.

Answers to the exercises can be found in Appendix A.

![](img/cf72ea860016d2d680fc085fc06f265a_134_0.png)

## Functions

## WHAT YOU WILL LEARN IN THIS CHAPTER

- Defining and using simple functions that don’t accept or return any data
- Transferring data to and from functions
- Working with variable scope
- Using command-line arguments with the `main()` function
- Supplying functions as members of struct types
- Using function overloading
- Using delegates

## WROX.COM CODE DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code downloads for this chapter at www.wrox.com/go/beginning_visualcsharp2015programming on the Download Code tab. The code is in the Chapter 6 download and individually named according to the names throughout the chapter.

All the code you have seen so far has taken the form of a single block, perhaps with some looping to repeat lines of code, and branching to execute statements conditionally. Performing an operation on your data has meant placing the code required right where you want it to work.

This kind of code structure is limited. Often, some tasks—such as finding the highest value in an array, for example—might need to be performed at several points in a program. You can place identical (or nearly identical) sections of code in your application whenever necessary, but this has its own problems. Changing even one minor detail concerning a common task (to correct a code error, for example) can require changes to multiple sections of code, which can be spread throughout the application. Missing one of these can have dramatic consequences and cause the whole application to fail. In addition, the application can get very lengthy.
