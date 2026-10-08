```
void test(int n)
{
    try {
        Vector v(n);
    }
    catch (std::length_error&) { // Il do something and rethrow
        cerr << "test failed: length error\n";
        throw; // Il rethrow
    }
    catch (std::bad_alloc&) { // Il touch! this program is not designed to handle memory exhaustion
        std::terminate(); // Il terminate the program
    }
}
```