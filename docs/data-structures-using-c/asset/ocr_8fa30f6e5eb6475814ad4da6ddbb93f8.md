```
void Push(float);
float TopElement();
Pop();
} S3, S4;
```

Here, s3 and s4 are stacks for storing real numbers. To avoid defining two similar stacks, which vary only in the type of data being processed, templates are used. When we need to perform the same operation on different data types, we can use function templates. Template is the most powerful feature of C++ that enables software reuse. Templates help in defining generic functions and classes. They allow the user to specify the type of data as a parameter.

Using templates, the two classes Intstack and Floatstack can be defined as a single class as follows:

```
template <class T>
class stack
{
    int Top;
    T Data[20];
    public:
    stack()
    {
        Top = -1;
    }
    void Push(T);
    T TopElement();
    Pop();
};
```

```
stack <int> S1, S2; // integer stacks
stack <float> S3, S4; // float stacks
```