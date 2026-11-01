```
int open_database(const char*);
void close_database(int);

int main()
{
    auto db = open_database("//network/customer.db");
}
```