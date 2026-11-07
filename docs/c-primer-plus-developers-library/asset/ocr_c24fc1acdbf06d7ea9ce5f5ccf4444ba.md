```
cout << num_strings << ": " << str
     << "\n" object created\n"; // For Your Information
}
```

What makes defining the copy constructor necessary is the fact that some class members are new-initialized pointers to data rather than the data themselves. Figure 12.3 illustrates deep copying.

![](bbox=[0.114, 0.265, 0.805, 0.824])

Figure 12.3  An inside look at deep copying.