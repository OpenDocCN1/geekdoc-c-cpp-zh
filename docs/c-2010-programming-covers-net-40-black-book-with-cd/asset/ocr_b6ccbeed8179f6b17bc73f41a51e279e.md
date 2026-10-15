# Implementing DOM in .NET

An XML document consists of a collection of nodes and attributes of the nodes. You can modify the data of an XML document by modifying the nodes or attributes. The System.Xml.XmlDocument class is used to implement the core XML DOM parser of the .NET Framework. You can use the DOM model implementation to modify the data of XML documents, by performing various tasks, such as inserting, deleting, or updating the data in the documents.

The DOM model is implemented by using the XmlNode and XmlNodeList classes. The XmlNode class is an abstract class that represents an XML document; while the XmlNodeList class represents an ordered list of nodes. Let’s use the XmlDataDocument, XmlDocument, XmlNode, XmlNodeList, XmlElement and XmlAttribute classes to implement the DOM model for modifying XML data. These classes belong to the System.Xml namespace.

In this heading, you learn how to find elements by their tag names and insert nodes in an XML document. To do so, we use the same XML file, authors.xml, in the applications created under the following sections.

# Finding Elements by Tag Name

You can retrieve elements from an XML document by using their tag names. Let’s create an application, named SearchElements (also available on the CD) to retrieve elements from an XML file.

Perform the following steps to create the SearchElements application:

+   1. Create a Windows Forms application, named SearchElements.
+   2. Add the authors.xml file in the bin\Debug folder of the SearchElements project.
+   3. Open the designer of the Form1 form and drag a list box and button from the Toolbox to it.
+   4. Set the Text property of the button to Show Elements.
+   5. Add the code given in Listing 30.5 to the Form1.cs file:

# Listing 30.5: Showing the Code of the Form1.cs File of the SearchElements Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Xml;

namespace SearchElements
{
    public partial class Form1 : Form
    {
        private XmlDocument xd = new XmlDocument();
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            listBox1.Items.Clear();
            xd.Load("authors.xml");
            XmlNodeList nl = xd.GetElementsByTagName("au_lname");
            foreach (XmlNode node in nl)
                listBox1.Items.Add(node.InnerText);
```