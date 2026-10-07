# Data Selection Query with C#.NET

![](bbox=[0.118, 0.085, 0.881, 0.413])

FIGURE 5.127 The opened and the finished object relation designer.

| LINQSPSelect Project | StudentForm() |
| --- | --- |
| using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Linq;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace SQLRetToObjectLINQ
{
public partial class StudentForm : Form
{
public StudentForm()
nInitializeComponent();
ComboName.Items.Add("Tom Erica");
ComboName.Items.Add("Ashly Jade");
ComboName.Items.Add("Emily Smith");
ComboName.Items.Add("Andrew Woods");
ComboName.Items.Add("Blue Valley");
ComboName.SelectedIndex = 0;
ComboMethod.Items.Add("LINQ to SQL Method");
ComboMethod.SelectedIndex = 0;
}
} |

FIGURE 5.128 The codes for the constructor of the StudentForm.