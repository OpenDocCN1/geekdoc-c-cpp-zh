```
{
    int a=1;
}
namespace ns2
{
    float a=3.33;
}
int main()
{
    {
        using namespace ns1;
        cout<<a<<endl;
    }
    {
        using namespace ns2;
        cout<<a<<endl;
    }
}
```

Output
1
3.33

# Namespaces aliases

One of the amazing features of namespace is that its alias can be created. So, after creating an alias the old name and new name both can be used.

The syntax for renaming the namespace is:

```
namespace new_name=old_name;
```