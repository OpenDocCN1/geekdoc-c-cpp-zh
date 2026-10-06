# 3.2 Inline Functions — 99

```
cout << "The values are ";ncout<<setw(5)<<count;
cout<<setw(5)<<index<<endl;
fiddle(count, index);
cout << "The values are ";ncout<<setw(5)<<count;
cout<<setw(5)<<index<<endl;
}
```

```
void fiddle(int in1, int &in2)
{
in1 = in1 + 100;
in2 = in2 + 100;
cout << "The values are ";
cout<<setw(5)<<in1;
cout<<setw(5)<<in2<<endl;
}
```

Running result:

| The values are 7 12 |
| The values are 107 112 |
| The values are 7 112 |

Analysis: The first parameter in1 of function fiddle has type int, and is assigned the value of the actual parameter count when the function is called. The second parameter in2 is a reference, and is initialized by the actual parameter index to an alias of index. Thus, the change on in1 in the called function has no effect on the actual parameter count, while the change on in2 in the called function is in fact the change on the variable index in the main function. When returned back to the main function, the value of count has not been changed, while the value of index has been changed.

# 3.2 Inline Functions

At the beginning of this chapter, we mentioned that using functions helps developers to reuse codes, improve the development efficiency and the reliability of the program, and facilitate the collaboration and modification of the program. But function calls can also reduce the execution efficiency of programs. When a call is made, the computer needs to save the execution scene and return address before jumping to the entry address of the called function and starting execution; when returned from the called function, the computer needs to restore the scene and return address previously saved before continuing the execution. These procedures take time and memory space.