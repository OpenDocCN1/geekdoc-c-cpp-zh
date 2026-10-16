```
ss.push_back(s[i]);
return ss;
}
```

Like vector, a string is really a handle to its elements. So, we simply move the ss out of reverse() rather than copying any elements (§3.3.2).

The resource management “smart pointers” (e.g., unique_ptr and smart_ptr) are a further example of these ideas (§5.2.1, §34.3.1). For example:

```
void f(int n)
{
int* p1 = new int[n]; // potential trouble unique_ptr<int[]> p2 {new int[n]};
```

```
// ...
if (n%2) throw runtime_error("odd");
delete[] p1; // we may never get here
}
```

For f(3) the memory pointed to by p1 is leaked, but the memory pointed to by p2 is correctly and implicitly deallocated.

My rule of thumb for the use of new and delete is “no naked new”; that is, new belongs in constructors and similar operations, delete belongs in destructors, and together they provide a coherent memory management strategy. In addition, new is often used in arguments to resource handles.

If everything else fails (e.g., if someone has a lot of old code with lots of undisciplined use of new), C++ offers a standard interface to a garbage collector (§34.5).

# 11.2.2 Arrays

Arrays of objects can also be created using new. For example:

```
char * save_string(const char* p)
{
char* s = new char[strlen(p)+1]; strcpy(s,p); // copy from p to s return s;
}
```

```
int main(int argc, char * argv[]) {
if (argc < 2) exit(1);
char* p = save_string(argv[1]);
// ...
delete[] p;
}
```

The “plain” operator delete is used to delete individual objects; delete[] is used to delete arrays. Unless you really must use a char* directly, the standard-library string can be used to simplify the save_string():