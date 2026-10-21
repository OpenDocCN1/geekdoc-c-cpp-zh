```
```cpp
cout << "\nEnter the data value of the last node :=";
cin >> value;
list.insert_end(value);
cout << "\nAfter insertion operation";
list.display();
}
```
```

# OUTPUT :

Enter the data terminated by negative number :
10 20 30 40 50 60 70 80 -3
Before any operation
Traversing in the forward direction :
10<->20<->30<->40<->50<->60<->70<->80<->NULL
Traversing in the back direction :
80<->70<->60<->50<->40<->30<->20<->10<->NULL
Enter the data value of the last node :=145
After insertion operation
Traversing in the forward direction :
10<->20<->30<->40<->50<->60<->70<->80<->145<->NULL
Traversing in the back direction :
145<->80<->70<->60<->50<->40<->30<->20<->10<->NULL

![](bbox=[0.247, 0.535, 0.755, 0.865])

Figure 15.20. *Output screen of the program.*