```
```cpp
string info = "\n\tThe Ballad of Reading Gaol" ;
info.append( "\n\t\tOscar Wilde 1898" );
// Add more statements here.
return 0 ;
}
```
```

+   3. In the main function, create an output filestream object – specifying a file mode that will append to existing text

```
```cpp
ofstream writer( "poem.txt" , ios::app );
```
```

+   4. Insert statements to append the string to a file or exit, then save, compile, and run the program to see the result

```
```cpp
if ( ! writer )
{
    cout << "Error opening file for output" << endl ;
    return -1 ;      // Signal an error then exit the program.
}
writer << info << endl ;      // Append output.
writer.close() ;              // Close filestream.
```
```

![](bbox=[0.31, 0.35, 0.689, 0.463])

![](bbox=[0.127, 0.491, 0.191, 0.538])

The file must allow the program suitable read and write permissions.