```
```cpp
int main()
{
    std::string s0;
    std::string s1{"short"};
    std::string s2{"a string with an extraordinarily long value"};
    std::cout << " s0 capa: " << s0.capacity() << " ('" << s0 << ")\n";
    std::cout << " s1 capa: " << s1.capacity() << " ('" << s1 << ")\n";
    std::cout << " s2 capa: " << s2.capacity() << " ('" << s2 << ")\n";

    std::string s3{std::move(s1)};
    std::string s4{std::move(s2)};
    std::cout << " s1 capa: " << s1.capacity() << " ('" << s1 << ")\n";
    std::cout << " s2 capa: " << s2.capacity() << " ('" << s2 << ")\n";
    std::cout << " s3 capa: " << s3.capacity() << " ('" << s3 << ")\n";
    std::cout << " s4 capa: " << s4.capacity() << " ('" << s4 << ")\n";

    std::string s5{"quite a reasonable value"};
    std::cout << " s4 capa: " << s4.capacity() << " ('" << s4 << ")\n";
    std::cout << " s5 capa: " << s5.capacity() << " ('" << s5 << ")\n";

    s4 = std::move(s5);
    std::cout << " s4 capa: " << s4.capacity() << " ('" << s4 << ")\n";
    std::cout << " s5 capa: " << s5.capacity() << " ('" << s5 << ")\n";
}
```
```

In this program, you can first see that usually empty strings have capacity for some characters due to the *small string optimization (SSO)*, which usually reserves 15 or 22 bytes for the value in the string itself. Beyond the size for SSO, the string allocates the memory on the heap, which has at least size necessary to store the value. Therefore, after

```
```cpp
std::string s0{};
std::string s1{"short"};
std::string s2{"a string with an extraordinarily long value"};
```
```

we might get something like one of the following outputs:

+   - Platform A:
+     - `s0 capa: 15 ('')`
+     - `s1 capa: 15 ('short')`
+     - `s2 capa: 43 ('a string with an extraordinarily long value')`
+   
+   - Platform B:
+     - `s0 capa: 22 ('')`
+     - `s1 capa: 22 ('short')`
+     - `s2 capa: 47 ('a string with an extraordinarily long value')`