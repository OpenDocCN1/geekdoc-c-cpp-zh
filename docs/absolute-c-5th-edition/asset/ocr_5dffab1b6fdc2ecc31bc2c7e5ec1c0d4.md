# Display 16.2 A Generic Sorting Function (part 2 of 2)

```
for (i = 0; i < 10; i++)
cout << a[i] << " ";
cout << endl;
sort(a, 10);
cout << "In sorted order the integers:\n";nfor (i = 0; i < 10; i++)
cout << a[i] << " ";
cout << endl;
double b[5] = {5.5, 4.4, 1.1, 3.3, 2.2};
cout << "Unsorted doubles:\n";nfor (i = 0; i < 5; i++)
cout << b[i] << " ";
cout << endl;
sort(b, 5);
cout << "In sorted order the doubles:\n";nfor (i = 0; i < 5; i++)
cout << b[i] << " ";
cout << endl;
char c[7] = {'G', 'E', 'N', 'E', 'R', 'I', 'C'};
cout << "Unsorted characters:\n";nfor (i = 0; i < 7; i++)
cout << c[i] << " ";
cout << endl;
sort(c, 7);
cout << "In sorted order the characters:\n";nfor (i = 0; i < 7; i++)
cout << c[i] << " ";
cout << endl;
```

```
return 0;
}
```

Sample Dialogue

Unsorted integers:

9 8 7 6 5 1 2 3 0 4

In sorted order the integers are:

0 1 2 3 4 5 6 7 8 9

Unsorted doubles:

5.5 4.4 1.1 3.3 2.2

In sorted order the doubles are:

1.1 2.2 3.3 4.4 5.5

Unsorted characters:

G E N E R I C

In sorted order the characters are:

C E E G I N R