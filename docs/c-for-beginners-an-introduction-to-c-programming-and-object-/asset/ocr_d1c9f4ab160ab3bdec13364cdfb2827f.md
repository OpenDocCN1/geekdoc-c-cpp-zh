```
```cpp
reverse[i] = reverse[j];
reverse[j] = temp;
j++;
}

cout << endl << endl
     << "Original : " << str << endl
     << "Reverse : " << reverse << endl;

if (strcmp(str, reverse) == ...)
    cout << "Palindrome" << endl;
else
    cout << "Not palindrome" << endl;

cout << endl << endl;
return;
}
```
```

Output:

![](bbox=[0.03, 0.44, 0.91, 0.72])