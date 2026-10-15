# Immediate Solutions

# Working with Collection Classes

In the In Depth section, you have learned to handle grouped data, simple arrays are sufficient most of the time. However, .NET collection classes provide more functionalities than arrays, such as sort and search operations. In this section, you learn to use the following classes:

+   - ArrayList
+   - Hashtable
+   - SortedList
+   - Stack
+   - Queue
+   - BitArray

Let’s learn how to use these classes, one by one.

# Using the ArrayList Class

As mentioned in the In Depth section, the ArrayList class provides an easy-to-use substitute for arrays. It provides various methods, such as Sort and Reverse, as well as allows you to change the size of an object dynamically. Let’s create a Windows Forms application named ArrayListSample, also available on the CD-ROM, to learn how to use the ArrayList class. This application contains a sample user interface form with three buttons—Create and add 10 items, Sort, and Search, and one ListBox control.

Perform the following steps to create and add elements to the ArrayList object:

+   1. Set the Text property of Form1 to ArrayList Sample in the ArrayListSample application.
+   2. Drag and drop a ListBox, a GroupBox, and three Button controls to the form.
+   3. Set the Text property of the GroupBox control to Noteworthy Operations and the Text property of button1 to Create and add 10 items, button2 to Sort, and button3 to Search.
+   4. Add the code given in Listing 32.1 in the Form1.cs file:

# Listing 32.1: Showing the Code of the ArrayListSample Application

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

namespace ArrayList_Sample
{
    public partial class Form1 : Form
    {
        private ArrayList ArrLst;
        public Form1()
        {
            InitializeComponent();
        }

        private void LoadArrList()
        {
            listBox1.Items.Clear();
```