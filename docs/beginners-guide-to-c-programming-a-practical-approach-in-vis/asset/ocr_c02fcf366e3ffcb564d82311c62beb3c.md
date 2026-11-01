associated array element, myStringArray[i, jj], is added to the ListBox by the code line arrayListBox.Items.Add(myStringArray[i, jj]);.

8. Build and run the project. The program window will be shown as in Figure 10.5. When the List elements Button is clicked, the elements of the array is written to the ListBox as in Figure 10.6.

![](bbox=[0.32, 0.32, 0.68, 0.62])

Figure 10.5. The program window

![](bbox=[0.32, 0.7, 0.68, 0.92])

Figure 10.6. Elements of the array listed in the ListBox

Note the order of elements in the ListBox. They are like [0, 0], [0, 1], [0, 2], [1, 0], ..., [1, 2]. As it can be seen from this order, i) the first loop