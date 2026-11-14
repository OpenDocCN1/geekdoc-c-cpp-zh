```
class vector_bool_proxy
{
    vector_bool_proxy& operator=(bool b)
    {
        if (b)
            byte|= mask;
        else
            byte&= ~mask;
        return *this;
    }
};
```