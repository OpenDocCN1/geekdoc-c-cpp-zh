```
```cpp
inflatable * ps = new inflatable; // allot memory for structure
cout << "Enter name of inflatable item: ";
cin.get(ps->name, 20);              // method 1 for member access
cout << "Enter volume in cubic feet: ";
cin >> (*ps).volume;                 // method 2 for member access
cout << "Enter price: $";
cin >> ps->price;
cout << "Name: " << (*ps).name << endl;         // method 2
cout << "Volume: " << ps->volume << " cubic feet\n"; // method 1
cout << "Price: $" << ps->price << endl;         // method 1
delete ps;                            // free memory used by structure
return 0;
}
```
```

Here is a sample run of the program in Listing 4.21:

```
```text
Enter name of inflatable item: Fabulous Frodo
Enter volume in cubic feet: 1.4
Enter price: $27.99
Name: Fabulous Frodo
Volume: 1.4 cubic feet
Price: $27.99
```
```

# An Example of Using new and delete

Let’s look at an example that uses new and delete to manage storing string input from the keyboard. Listing 4.22 defines a function getname() that returns a pointer to an input string. This function reads the input into a large temporary array and then uses new [] with an appropriate size to create a chunk of memory sized to fit to the input string. Then the function returns the pointer to the block. This approach could conserve a lot of memory for programs that read in a large number of strings. (In real life, where many of us live, it would be easier to use the string class, which has the use of new and delete built in to its design.)

Suppose your program has to read 1,000 strings and that the largest string might be 79 characters long, but most of the strings are much shorter than that. If you used char arrays to hold the strings, you’d need 1,000 arrays of 80 characters each. That’s 80,000 bytes, and much of that block of memory would wind up being unused. Alternatively, you could create an array of 1,000 pointers to char and then use new to allocate only the amount of memory needed for each string. That could save tens of thousands of bytes. Instead of having to use a large array for every string, you fit the memory to the input. Even better, you could also use new to find space to store only as many pointers as needed. Well, that’s a little too ambitious for right now. Even using an array of 1,000 pointers is a little too ambitious for right now, but Listing 4.22 illustrates some of the technique. Also just to illustrate how delete works, the program uses it to free memory for reuse.