```
cout << "Now let us swap record no. 1 with record no. 3 \n";
CustomerFile.seekp(0, ios::beg);
CustomerFile.write((char *) &Answer2, sizeof(customer));

CustomerFile.seekp(2 * sizeof(customer), ios::beg);
CustomerFile.write((char *) &Answer1, sizeof(customer));
cout << "After seekp() is moved to the end of the second record \n";

cout << "The get pointer is at byte no. " << CustomerFile.tellg() << endl;
cout << "The put pointer is at byte no. " << CustomerFile.tellp() << endl;
cout << "Swapped record no. 1 is as follows \n";
CustomerFile.seekg(0, ios::beg);
CustomerFile.read((char *) &Answer1, sizeof(customer));
cout << Answer1;

cout << "Swapped record no. 3 is as follows \n";
CustomerFile.seekg(2 * sizeof(customer), ios::beg);
CustomerFile.read((char *) &Answer2, sizeof(customer));
cout << Answer2;

CustomerFile.close();
return 0;
}
```

# Output

Initial stage
The get pointer is at byte no. 96
The put pointer is at byte no. 96

After seekg() is moved to the beginning of the file
The get pointer is at byte no. 0
The put pointer is at byte no. 0

Record no. 1 is as follows
1 Brian Charles Lara

Record no. 3 is as follows
3 Steffi Graf

After seekg() is moved to the end of the second record
The get pointer is at byte no. 96
The put pointer is at byte no. 96
3 Steffi Graf

Now let us swap record no. 1 with record no. 3

After seekp() is moved to the end of the second record
The get pointer is at byte no. -1
The put pointer is at byte no. -1

Swapped record no. 1 is as follows
1 Brian Charles Lara

Swapped record no. 3 is as follows
3 Steffi Graf

# Notes

+   1. Changing the put pointer changes the value of the get pointer and vice versa. Although mentioned as two different pointers, get for read and put for write, they refer to a single pointer, as in C.
+   2. Regardless of what pointer we use (seekg() or seekp()), the other pointer moves with it. At any given point of time, both read and write pointers point to a single location of the file.