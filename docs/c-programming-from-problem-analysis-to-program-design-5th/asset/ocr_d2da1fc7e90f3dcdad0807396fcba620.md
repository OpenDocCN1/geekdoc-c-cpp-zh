Consider the following C++ program:

```
```cpp
1.  #include <iostream>
2.
3.  using namespace std;
4.
5.  int main()
6.  {
7.      int num
8.
9.      num = 18;
10.
11.     tempNum = 2 * num;
12.
13.     cout << "Num = " << num << ", tempNum = " << tempNum << endl;
14.
15.     return ;
16. }
```
```

(Note that the numbers 1 to 16 on the left side are not part of the program. We have numbered the statements for easy references.) This program contains syntax errors. When you compile this program, the compiler produces the following errors: (This program is compiled using Visual C++ Express 2008.)

```
```
Example2_Syntax_Errors.cpp
c:\chapter 2 source code\example2_syntax_errors.cpp(9) : error C2146: syntax error :
missing ';' before identifier 'num'
c:\chapter 2 source code\example2_syntax_errors.cpp(11) : error C2065: 'tempNum' :
undeclared identifier
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2065: 'tempNum' :
undeclared identifier
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2563: mismatch in formal
parameter list
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2568: '<<' : unable to
resolve function overload
    c:\program files\microsoft visual studio 9.0\vc\include\ostream(974) : could be
'std::basic_ostream<_Elem,_Traits> &std::endl(std::basic_ostream<_Elem,_Traits> &)'
        with
            [
                _Elem=wchar_t,
                _Traits=std::char_traits<wchar_t>
            ]
    c:\program files\microsoft visual studio 9.0\vc\include\ostream(966) : or
'std::basic_ostream<_Elem,_Traits> &std::endl(std::basic_ostream<_Elem,_Traits> &)'
        with
            [
                _Elem=char,
                _Traits=std::char_traits<char>
            ]
```
```

![](bbox=[0.929, 0.161, 0.999, 0.269])