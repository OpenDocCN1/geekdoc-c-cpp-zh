Here’s a sample run of the program in Listing 17.20, based on a planets.dat file that has had a few more entries added since you last saw it:

```
```
Here are the current contents of the planets.dat file:
0:          Earth: 6928198253 9.81
1:          Jenny's World: 32155648 8.93
2:          Tranter: 8900000000 15.03
3:          Trellan: 5214000 9.62
4:          Preestone: 3945851000 8.68
5:          Taanagoot: 361000004 10.23
6:          Marin: 252409 9.79
Enter the record number you wish to change: 2
Your selection:
        Tranter: 8900000000 15.03
Enter planet name: Tranter
Enter planetary population: 89521844777
Enter planet's acceleration of gravity: 10.53
Here are the new contents of the planets.dat file:
0:          Earth: 6928198253 9.81
1:          Jenny's World: 32155648 8.93
2:          Tranter: 89521844777 10.53
3:          Trellan: 5214000 9.62
4:          Preestone: 3945851000 8.68
5:          Taanagoot: 361000004 10.23
6:          Marin: 252409 9.79
Done.
```
```

By using the techniques in this program, you can extend it so that it allows you to add new material and delete records. If you were to expand the program, it would be a good idea to reorganize it by using classes and functions. For example, you could convert the planet structure to a class definition; then you could overload the << insertion operator so that cout << pl displays the class data members formatted as in the example. Also the example doesn’t bother to verify input, so you could add code to check for numeric input where appropriate.

# ### Working with Temporary Files

Developing applications often requires the use of temporary files whose lifetimes are transient and must be controlled by the program. Have you ever thought about how to go about this in C++? It's really quite easy to create a temporary file, copy the contents of another file, and delete the file. First of all, you need to come up with a naming scheme for your temporary file(s). But wait...how can you ensure that each file is assigned a unique name? The tmpnam() standard function declared in cstdio you have covered:

```
```
char* tmpnam( char* pszName );
```
```

The tmpnam() function creates a temporary name and places it in the C-style string that is pointed to by pszName. The constants L_tmpnam and TMP_MAX, both defined in cstdio,