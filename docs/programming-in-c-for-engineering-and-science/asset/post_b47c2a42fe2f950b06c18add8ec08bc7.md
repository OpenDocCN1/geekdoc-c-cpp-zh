
5. month, day, year
6. display()

7. birth.display();

## Section 7.3
- 1. Bjarne Stroustrup
- 2. Jerry Schwarz
- 3. istream and ostream
- 4. stream
- 5. istream
- 6. cin
- 7. good, bad, and fail
- 8. good()
- 9. clear()
- 10. ignore()
- 11. true
- 12. false
- 13. ostream
- 14. cout
- 15. endl, flush
- 16. true
- 17. false

## Section 7.4
- 1. empty
- 2. string label;
- 3. const string UNITS = "meters";
- 4. "ABC", "DEF"
- 5. 'e'
- 6. 8
- 7. 0
- 8. false
- 9. true
- 10. true
- 11. false
- 12. seashoreshell
- 13. "she"
- 14. 10
- 15. 27
- 16. 12
- 17. 29
- 18. 0
- 19. 35
- 20. "bell"
- 21. "seal on the shore"
- 22. "She sells the seashore."

## Section 7.5
- 1. 15 + 5i
- 2. 50 + 37i
- 3. 55 + 48i
- 4. 1 + i
- 5. (62/53) + (5/53)i ≈ 1.1698 + .09434i
- 6. √73 ≈ 8.544

## CHAPTER 8
### Section 8.2
- 1. 198
  197
  default
- 2. 198
- 3. default
- 4. default
- 5. -2
  default
- 6. -2
- 7. 123
- 8. 456
- 9. no output produced
- 10. error—x must be integer (or integer compatible)

## CHAPTER 9
### Section 9.4
- 1. counting (or counter-controlled) loops, for
- 2. initialization expression, loop condition, step expression, loop body
- 3. if-break (or if-return)
- 4. pretest
- 5. posttest
- 6. posttest
- 7. pretest
- 8. 2*0 = 0
  2*1 = 2
  2*2 = 4
  2*3 = 6
  2*4 = 8
  2*5 = 10
  2*6 = 12
  2*7 = 14
  2*8 = 16
  2*9 = 18
- 9. 1 3 5 7 9 11
- 10. 11
  22
  1
  33
  2
  1
- 11. 000
  112
  228
  18
- 12. 4
  5
  228
  18

## Section 9.6
- 1. sentinel, counting, query-controlled
- 2. end-of-data flag, sentinel
- 3. true
- 4. end-of-file (or eof)
- 5. eof()
- 6. false
- 7. false
- 8. query

## CHAPTER 10
### Section 10.3
- 1. value
- 2. value
- 3. value
- 4. reference
- 5. ampersand (&)
- 6. false
- 7. true
- 8. false
- 9. false
- 10. false

```
void f(const int & x, int & y, int & z)
{
    z = y = x * x + 1;
}
```

12. String = batbatelk

### Section 10.5
- 1. scope
- 2. false
- 3. end of the block
- 4. the body of the function
- 5. scope error message (perhaps a warning)
- 6. signature
- 7. name
- 8. signature
- 9. template
- 10. type

13. 3
2
1
0
-1
14. 0 1
1 2
2 5

14.(continued)
3 10
4 17
*****
15. 4 12
3 5
2 0
1 -3

## CHAPTER 11
### Section 11.2
- 1. istream, cin
- 4. ostream
- 2. ostream, cout (or cerr)
- 5. fstream
- 3. istream
- 6. false

```
7. ifstream inputStream;
   inputStream.open("EmployeeInfo");
```

```
8. ifstream inputStream("EmployeeInfo");
```

```
9. ofstream outputStream;
   outputStream.open("EmployeeReport");
```

```
10. ofstream outputStream("EmployeeReport");
```

```
11. string inFileName, outFileName;
    cout << "Name of input file? ";
    cin >> inFileName;
    ifstream inputStream;
    inputStream.open(inFileName.data());
    or replace the last two lines with:
    ifstream inputStream(inFileName.data());
```

12. false

13. true

```
14. assert(inputStream.is_open());
```

15. get_line(inputStream, str); where str is of type string

```
16. if (inputSteam.eof())
    cout << "End of file\n";
```

```
17. inputStream.close();
```

### Section 11.3
- 1. false
- 3. random
- 2. true
- 4. tellg(), seekg()
- 5. inputStream.seekg(3, ios::beg());

```
6. inputStream.seekg(3, ios::cur());
```

```
7. inputStream.seekg(0, ios::end());
```

```
8. char ch;
    inputStream.get(ch);
    cout << ch;
```

```
9. char ch;
    inputStream.peek(ch);    or    inputStream.get(ch);
    cout << ch;                cout << ch;
                            inputStream.putback(ch);
```

10. formatting manipulators

## CHAPTER 12
### Section 12.2
- 1. false
- 2. false (not necessarily)
- 3. true
- 4. false
- 5. true
- 6. false
- 7. false
- 8. 5
- 9. true
- 10. true
- 11. true
- 12. false
- 13. true
- 14. base
- 15. false
- 16. true
- 17. false
- 18. reference
- 19. xValue[0]: 0.0
  xValue[1]: 0.5
  xValue[2]: 1.0
  xValue[3]: 1.5
  xValue[4]: 2.0
- 20. number[0]: 0
  number[1]: 3
  number[2]: 4
  number[3]: 7
  number[4]: 8
- 21. number[0]: 1
  number[1]: 2
  number[2]: 4
  number[3]: 8
  number[4]: 16
- 22. number[0]: 0
  number[1]: 0
  number[2]: 0
  number[3]: 0
  number[4]: 0

### Section 12.6
- 1. int
- 2. 0, 0
- 3. 5, 5
- 4. 5, 5

## CHAPTER 13
### Section 13.2
- 1. two-dimensional
- 2. three-dimensional
- 3. square
- 4. 82
- 5. 33
- 6. -1
- 7. 33
- 8. 12
- 9. 1, 2, 3, 4
- 10. 52
- 11. 76
- 12. 29
- 13. 1322
- 14. 1322

### Section 13.4
- 1. m × n matrix
- 2. 2, 2
- 3. [[5, 2], [8, 8]]
- 4. [[1, 2, 0], [1, 3, 3], [10, 5, 9]]
5. Not defined—number of columns in B ≠ number of rows in C
6. Not defined—number of columns in C ≠ number of rows in B
- 7. [[4, 2], [3, -1], [9, 1]]
- 8. [[-2, -2], [1, -1], [2, 5]]

### Section 13.6
- 1. true
- 2. true
- 3. 5, 4
- 4. qqTab[1][3] = 1.1;
- 5. 5
- 6. 4
- 7. qqTab[1].push_back(99.9);
- 8. TableRow bottom(4, 0.0);
  qqTab.push_back(bottom);

## CHAPTER 14
### Section 14.2
- 1. class, class library
- 2. design, implementation
- 3. Its behavior and its attributes
- 4. behavior
- 5. I-can-do-it-myself

### Section 14.3
- 1. data, instance
- 2. Encapsulation
- 3. Items in the public section are accessible to users of the class, but those in the private section are not. By preventing a program from directly accessing the data members of a class, we hide that information, thus removing the temptation to access those variables directly.
- 4. private
- 5. invariant
- 6. function, methods
- 7. name of the class, scope (::)
- 8. constant, const
- 9. Fraction
- 10. Default-value constructors: used to initialize data members with default values when none are specified in the declaration of an object; explicit-value constructors initialize them with values provided in the declaration.
- 11. False—constructors have no return type
- 12. public

## CHAPTER 15
### Section 14.6
- 1. friend
- 2. preprocessor
- 3. #
- 4. conditional-compilation
5. The declaration of the class with the specified name will only be processed once, regardless of how many different files include it.

### Section 15.1
- 1. address
- 2. &
- 3. *
- 4. address
- 5. double value
- 6. address
- 7. address
- 8. double value
- 9. double value
- 10. address
- 11. null
- 12. 1.1
- 13. 3.3
- 14. true
- 15. true
- 16. 012a50

### Section 15.2
- 1. compile, run
- 2. new, null address, address, anonymous
- 3. delete
- 4. pointer variable
- 5. 66
- 13. postcondition
- 14. dot, message
- 15. accessor
- 16. operator+

```
17. class Component
{
    public:
        void display(ostream & out);
        void read(istream & in);
    private:
        int myID;
        string myName;
};
```

### Section 15.3
- 1. true
- 4. null
- 2. nodes, pointers
- 5. false
- 3. data, next
- 6. true

## CHAPTER 16
### Section 16.1
- 1. 10011010010
- 6. adapter
- 2. 2322
- 7. 123
- 3. 4D2
- 8. 111, 111
- 4. first, LIFO (last in, first out)
- 9. 0, 2, 4
- 5. empty, push, top, pop

### Section 16.3
- 1. For a queue, elements are added at one end and removed at the other. For a stack, elements are added and removed at the same end.
- 2. last
- 6. deque
- 3. FIFO
- 7. 456
- 4. spool
- 8. 222, 111
- 5. buffers
- 9. 4, 6, 8

### Section 16.4
- 1. root
- 4. at most two children
- 2. leaves
- 5. 50
- 3. children, parent
- 6. 10, 40, 70
- 7.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_706_0.png)

8.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_707_0.png)

9.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_707_1.png)

10.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_707_2.png)

11. 10, 20, 30, 40, 50, 60, 70, 80, 90, 100

12. 90, 30, 20, 10, 60, 50, 40, 70, 90, 100

13. 10, 20, 40, 50, 70, 60, 30, 100, 90, 80
