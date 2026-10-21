```
public:
    Type *operator[](int Index)
    {
        if((Index < 0) || (Index > Size - 1))
        {
            cout << "Subscript out of range!";
            exit(1);
        }
        else
        {
            cout << "Element no. " << Index << " is accessed \n";
            return Array[Index];
        }
    }
};
int main()
{
    SafeGenericArray <int> SafeIntArray1;
    SafeGenericArray <char> SafeCharArray1;
    
    SafeGenericArray <char *> SafeStringArray;
    char *String = "Lara";
    strcpy(SafeStringArray[1], String);
    SafeIntArray1[0] = 5;
    return 0;
}
```

# Output

Element no. 1 is accessed

We can also have multiple partial specializations for a single primary specialization, that is, we can have class SafeGenericArray <type &>, etc.

# 7.4 COMPILATION MODELS FOR TEMPLATES

When templates are included in the programs, there are two different ways to compile them. One is similar to inline functions where the template body is included when the templates are called; the other is similar to normal functions where the function call is replaced by some sort of jump instruction that calls the template function for a specified type and the control gets transferred to that place. Here we discuss both the types of compilation models.

# 7.4.1 Inline vs Non-inline Function Calls in Multiple Files

A very important difference between inline functions and normal functions is the way they are defined in a multifile program. It is possible to have a program that contains multiple files. Assume that Prog1.cpp, Prog2.cpp, and Prog3.cpp are three different files containing three different parts of the same program. To execute the program, the individual files are compiled one after another and then all the files are linked together to build a single executable file.

Suppose there is an inline function call in Prog1.cpp and Prog3.cpp. A copy of the function is needed in both the files. This is because inline functions are pasted at the time of compilation. If the individual file does not contain the body of the inline function, they cannot replace the call with the body.