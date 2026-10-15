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