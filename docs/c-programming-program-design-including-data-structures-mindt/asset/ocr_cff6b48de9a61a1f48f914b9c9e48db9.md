```
    for (auto &str: names)
    {
        pos = str.find(ch);
        length = str.length();
        str1 = str.substr(0, pos);
        str2 = str.substr(pos + 2, length - pos - 1);
        str = str2 + ' ' + str1;
    }

    for (auto str: names)
        cout << str << endl;
```

33. Consider the following function heading. (9, 10)

```
    void modifyList(int list[], int length)
```

In the definition of the function modifyList, can you use a range-based for loop to process the elements of list? Justify your answer.

34. Given the declaration:

```
    char name[30] ;
```

mark the following statements as valid or invalid. If a statement is invalid, explain why. (11)

+   a. `name = "Bill William";`
+   b. `strcmp(name, "Tom Jackson");`
+   c. `strcpy(name, "Jacksonville");`
+   d. `cin >> name;`
+   e. `name[0] = 'K';`
+   f. `bool flag = (name >= "Cynthia");`

35. Given the declaration:

```
    char str1[20];
    char str2[15] = "Fruit Juice";
```

mark the following statements as valid or invalid. If a statement is invalid, explain why. (11, 12)

+   a. `strcpy(str1, str2);`
+   b. `if (strcmp(str1, str2) == 0)`
+      `cout << " str1 is the same as str2" << endl;`
+   c. `if (strlen(str1) >= strlen(str2))`
+      `str1 = str2;`
+   d. `if (str1 > str2)`
+      `cout << "str1 > str2." << endl;`

36. Given the declaration:

```
    char name[8] = "Shelly";
```