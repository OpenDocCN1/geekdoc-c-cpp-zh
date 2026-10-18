```
```cpp
exit(0);
}
k++;
}
else
break;
}
}
if(i==len)
cout<<"\nThe substring is not present in the main string";
getch();
}
```
```

The output of Program 9.6 would be:

The main string is:
C++ is better than C
Enter the substring to be searched: bet
The substring is present in the main string

# Pointers to Functions

Even though pointers to functions (or function pointers) are introduced in C, they are widely used in C++ for dynamic binding, and event-based applications. The concept of pointer to function acts as a base for pointers to members, which we have discussed in Chapter 5.

The pointer to function is known as callback function. We can use these function pointers to refer to a function. Using function pointers, we can allow a C++ program to select a function dynamically at run