```
{
    InitializeComponent();
}
private void button1_Click(object sender, EventArgs e)
{
    Q = new Queue(10);
    Q.Enqueue("white");
    Q.Enqueue("Black");
    Q.Enqueue("Blue");
    Q.Enqueue("Yellow");
    Q.Enqueue("Green");
    Q.Enqueue("Red");
    Q.Enqueue("Orange");
    Q.Enqueue("Purple");
    Q.Enqueue("Magenta");
    Q.Enqueue("Brown");
    LoadQ();
    button2.Enabled = true;
    button3.Enabled = true;
}
private void Form1_Load(object sender, EventArgs e)
{
    button2.Enabled = false;
    button3.Enabled = false;
}
private void LoadQ()
{
    listBox1.Items.Clear();
    object[] objArr = Q.ToArray();
    for (int i = 0; i < Q.Count; i++) {
        listBox1.Items.Add(objArr[i]);
    }
}
private void button2_Click(object sender, EventArgs e)
{
    Q.Enqueue(Microsoft.VisualBasic.Interaction.InputBox("Enter the value for the item to be enqueued.", "", "", -1, -1));
    LoadQ();
}
private void button3_Click(object sender, EventArgs e)
{
    MessageBox.Show(Q.Dequeue().ToString(), "Item dequeued.");
    LoadQ();
}
}
```

In Listing 32.5, the Enqueue and Dequeue methods are used to add and remove elements from a Queue object. The Click event of button1 creates a Queue object, Q. This object is populated with 10 elements by using the Enqueue method. The Click event of button2 control also uses the Enqueue method to add a new element in a Queue object at runtime. Further, the Click event of button3 is used to remove an element from the Queue object by using the Dequeue method.

5. Press the F5 key to execute the application. When the form appears, click the Create and add 10 items button. The Queue object is created and 10 elements are added to it. These elements are the names of different colors that are added to the ListBox control, as shown in Figure 32.23:

## Chapter 32: Collections and Generics

![](img/e073a4882197be4ab61103cbe0bcb394_1547_0.png)

**Figure 32.23: Creating and Adding 10 Elements to the Queue Object**

When you click the Enqueue button, an input box appears, prompting you to enter the item that you want to add to the Queue object, as shown in Figure 32.24:

![](img/e073a4882197be4ab61103cbe0bcb394_1547_1.png)

**Figure 32.24: Adding an Element to the Queue Object**

Enter a color name, for instance Aqua, and click the OK button. The new item is added at the end of the ListBox control, as shown in Figure 32.25:

![](img/e073a4882197be4ab61103cbe0bcb394_1547_2.png)

**Figure 32.25: Displaying the Newly Added Item in the ListBox Control**

To remove an item from the ListBox control, click the Dequeue button. A message box appears with the name of the item that is to be removed from the list, as shown in Figure 32.26:

![](img/e073a4882197be4ab61103cbe0bcb394_1548_0.png)

Figure 32.26: Displaying an Element Name for Dequeue

## Using the BitArray Class

The BitArray class allows you to store elements in a binary format. The bit value 0 for an element implies the False value, while the bit value 1 for an element implies the True value. You are allowed to perform various operations, such as XOR, AND, and NOT directly on these values. Let’s create an application named BitArraySample, also available on the CD-ROM, which uses the BitArray class. This application contains a sample user interface form with three buttons—Create and add 10 items, Xor, and Not, and a ListView control.

Perform the following steps to create the BitArraySample application:

- 1. Set the Text property of Form1 to BitArray Sample in the BitArraySample application.
- 2. Drag and drop a ListView, a GroupBox, and three Button controls to the form.
- 3. Set the Text property of the GroupBox control to Noteworthy Operations and the Text property of button1 to Create and add 10 items, button2 to Xor, and button3 to Not.
- 4. Add the code given in Listing 32.6 to the Form1.cs file of the BitArraySample application:

Listing 32.6: Showing the Code of the BitArraySample Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Collections;

namespace BitArraysSample
{
public partial class Form1 : Form
{
    public BitArray BitArr1, BitArr2;
    public Form1()
    {
        InitializeComponent();
    }
    private void button1_Click(object sender, EventArgs e)
    {
        BitArr1 = new BitArray(10);
        BitArr1.Set(0, false);
        BitArr1.Set(1, false);
BitArr1.Set(2, true);
BitArr1.Set(3, true);
BitArr1.Set(4, true);
BitArr1.Set(5, true);
BitArr1.Set(6, false);
BitArr1.Set(7, false);
BitArr1.Set(8, true);
BitArr1.Set(9, false);
LoadBtArr();
button2.Enabled = true;
button3.Enabled = true;
}
private void LoadBtArr()
{
    listview1.Clear();
    listview1.BackColor = Color.Black;
    listview1.ForeColor = Color.White;
    for (int i = 0; i < BitArr1.Count; i++)
    {
        listview1.Items.Add(BitArr1[i].ToString());
    }
}
private void Form1_Load(object sender, EventArgs e)
{
    button2.Enabled = false;
    button3.Enabled = false;
}
private void button2_Click(object sender, EventArgs e)
{
    BitArr2 = new BitArray(10);
    BitArr2.SetAll(true);
    BitArr1.Xor(BitArr2);
    LoadBtArr();
}
private void button3_Click(object sender, EventArgs e)
{
    BitArr1.Not();
    LoadBtArr();
}
}
```

In Listing 32.6, the Set method is used to add elements to the BitArray object. This method takes two parameters--one is the index number for the item and second is the Boolean value for the BitArray object. The Xor method performs the bitwise exclusive OR operation on the elements of BitArray object to a specific BitArray object value that is specified by using the SetAll method. The Not method inverts all the bit values of the current object of the BitArray class, so that elements that are set to true are changed to false, and the elements that are set to false are changed to true. These methods are used in the Click events of the button1, button2, and button3 controls.

- 5. Press the F5 key to execute the application. When the form appears, click the Create and add 10 item button. The BitArray object is created and 10 elements are added to it, which you can see in the ListView control, as shown in Figure 32.27:

![](img/e073a4882197be4ab61103cbe0bcb394_1550_0.png)

# Figure 32.27: Creating and Adding 10 Elements to the BitArray Object

Now, click the Xor button to perform XOR operation on each element value with the specified value True. The result is displayed, as shown in Figure 32.28:

![](img/e073a4882197be4ab61103cbe0bcb394_1550_1.png)

# Figure 32.28: Displaying the Result of the XOR Operation

Further, if you click the Not button, all the bit values are inverted, as shown in Figure 32.29:

![](img/e073a4882197be4ab61103cbe0bcb394_1550_2.png)

# Figure 32.29: Displaying the Result of the NOT Operation

Let’s now learn to work with the generic collection classes.

## Working with Generic Collection Classes

.NET Framework provides the System.Collections.Generic namespace that contains a number of generic collection classes. Many generic collection types have direct correlation with non-generic types. For example, the List<T> class is a generic version of the ArrayList collection class. You will find generic as well as non-generic versions of the SortedList class that are a combination of the Dictionary<T> and List<T> classes. The Dictionary<T> class is a generic version of the Hashtable class. The Queue<T> and Stack<T> classes are the generic version of Queue and Stack collection classes. Now, let’s discuss these generic classes in detail.

## Using the List<T> Class

The List<T> class contains properties that act as an array. The difference, however, is that it expands automatically as elements are added. You can also shrink the size of an object of this by class using the TrimToSize method or the Capacity property. You can access each item of the List<T> object using its index value. Let’s create a Windows Forms application named GenericListSample, also available on the CD ROM, to show the use of the List<T> class. This application contains a sample user interface form with four buttons—Create and adds 10 elements, Insert, Remove, and Reverse, and also contains a ListBox control.

Perform the following steps to create this application:

- 1. Set the Text property of Form1 to Generic List Sample in the GenericListSample application.
- 2. Drag and drop a ListBox, a GroupBox, and four Button controls to the form.
- 3. Set the Text property of the GroupBox control to Noteworthy Operations and the Text property of button1 to Create and add 10 items, button2 to Insert, button3 to Remove, and button4 to Reverse.
- 4. Add the code, given in Listing 32.7, in the Form1.cs file of the GenericListSample application:

# Listing 32.7: Showing the Code of the GenericListSample Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace GenericListSample
{
public partial class Form1 : Form
{
    List<string> LstStr = new List<string>();
    public Form1()
    {
        InitializeComponent();
    }
    private void Form1_Load(object sender, EventArgs e)
    {
        button2.Enabled = false;
        button3.Enabled = false;
        button4.Enabled = false;
    }
    private void button1_Click(object sender, EventArgs e)
    {
        LstStr.Add("white");
        LstStr.Add("Black");
        LstStr.Add("Blue");
        LstStr.Add("Yellow");
        LstStr.Add("Green");
```
