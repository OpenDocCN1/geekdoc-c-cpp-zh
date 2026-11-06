```
```cpp
// write user-specified information in file
outCredit.write(
    reinterpret_cast<const char *>(&client), sizeof(ClientData));

// enable user to enter another account
cout << "Enter account number\n? ";
cin >> accountNumber;
}
}
```
```

![](bbox=[0.118, 0.252, 0.881, 0.588])

# Fig. 14.11 Writing to a random-access file.

# 14.9.1 Opening a File for Input and Output in Binary Mode

Line 10 uses the `fstream` object `outCredit` to open the existing `credit.dat` file. The file is opened for input and output in *binary mode*.