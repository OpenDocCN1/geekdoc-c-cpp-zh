# # Part II: Application Development Using C#

![](bbox=[0.151, 0.089, 0.755, 0.439])

Figure 16-14

Switch to the code-behind of Form1, and import the following namespace:

```
```csharp
using System.Drawing.Printing;
```
```

Declare the following member variables:

```
```csharp
public partial class Form1 : Form
{
    //---constants for the icon images---
    const int ico_OPEN = 0;
    const int ico_CLOSE = 1;
    const int ico_PHOTO = 2;

    //---font variables---
    Font f_title;
    Font f_body;

    //---page counter---
    int pagecounter;

    //---PrintDocument variable---
    PrintDocument printDoc;
```
```