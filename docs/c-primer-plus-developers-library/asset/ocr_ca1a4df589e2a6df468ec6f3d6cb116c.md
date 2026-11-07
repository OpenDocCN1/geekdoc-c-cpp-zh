```
~~~cpp
class hold;
hold<T> q;
hold<int> n;
public:
    beta( T t, int i) : q(t), n(i) {}
    template<typename U>   // declaration
    U blab(U u, T t);
    void Show() const { q.show(); n.show();}
};
~~~
```

```
~~~cpp
// member definition
template <typename T>
    template<typename V>
        class beta<T>::hold
        {
        private:
            V val;
        public:
            hold(V v = 0) : val(v) {}
            void show() const { std::cout << val << std::endl; }
            V Value() const { return val; }
        };
~~~
```

```
~~~cpp
// member definition
template <typename T>
    template <typename U>
        U beta<T>::blab(U u, T t)
        {
            return (n.Value() + q.Value()) * u / t;
        }
~~~
```

The definitions have to identify T, V, and U as template parameters. Because the templates are nested, you have to use the

```
~~~cpp
template <typename T>
    template <typename V>
~~~
```

syntax instead of this syntax:

```
~~~cpp
template<typename T, typename V>
~~~
```

The definitions also must indicate that hold and blab are members of the beta<T> class, and they use the scope-resolution operator to do so.

# Templates As Parameters

You've seen that a template can have type parameters, such as typename T, and non-type parameters, such as int n. A template can also have a parameter that is itself a