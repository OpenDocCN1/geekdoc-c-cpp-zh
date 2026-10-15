```
```cpp
// function to create objects
void create( void )
{
    cout << "\\nCREATE FUNCTION: EXECUTION BEGINS" << endl;
    CreateAndDestroy fifth( 5, "local automatic in create" );
    static CreateAndDestroy sixth( 6, "local static in create" );
    CreateAndDestroy seventh( 7, "local automatic in create" );
    cout << "\\nCREATE FUNCTION: EXECUTION ENDS" << endl;
} // end function create
```
```

```
```
Object 1   constructor runs   (global before main)

MAIN FUNCTION: EXECUTION BEGINS
Object 2   constructor runs   (local automatic in main)
Object 3   constructor runs   (local static in main)

CREATE FUNCTION: EXECUTION BEGINS
Object 5   constructor runs   (local automatic in create)
Object 6   constructor runs   (local static in create)
Object 7   constructor runs   (local automatic in create)

CREATE FUNCTION: EXECUTION ENDS
Object 7   destructor runs    (local automatic in create)
Object 5   destructor runs    (local automatic in create)

MAIN FUNCTION: EXECUTION RESUMES
Object 4   constructor runs   (local automatic in main)

MAIN FUNCTION: EXECUTION ENDS
Object 4   destructor runs    (local automatic in main)
Object 2   destructor runs    (local automatic in main)

Object 6   destructor runs    (local static in create)
Object 3   destructor runs    (local static in main)

Object 1   destructor runs    (global before main)
```
```

**Fig. 9.13** | Order in which constructors and destructors are called. (Part 2 of 2.)

Function main (lines 14–26) declares three objects. Objects second (line 17) and fourth (line 23) are local automatic objects, and object third (line 18) is a static local object. The constructor for each of these objects is called when execution reaches the point where that object is declared. The destructors for objects fourth and then second are called (i.e., the reverse of the order in which their constructors were called) when execution reaches the end of main. Because object third is static, it exists until program termination. The destructor for object third is called before the destructor for global object first, but after all other objects are destroyed.

Function create (lines 29–36) declares three objects—fifth (line 32) and seventh (line 34) as local automatic objects, and sixth (line 33) as a static local object. The destructors for objects seventh and then fifth are called (i.e., the reverse of the order in which their constructors were called) when create terminates. Because sixth is static, it exists until program termination. The destructor for sixth is called before the destructors for third and first, but after all other objects are destroyed.