```
template<typename... T>
typename enable_if<(N<sizeof...(T))>::type
print(ostream& os, const tuple<T...>& t) const // nonempty tuple
{
os << ", " << get<N>(t); // print an element print_tuple<N+1>()(os,t); // print the rest of the elements
}

template<typename... T>
typename enable_if<!(N<sizeof...(T))>::type // empty tuple
print(ostream&, const tuple<T...>&) const
{
}
};
```

The pattern is that of a recursive function with a terminating overload (like printf() from §28.6.1). However, note how it wastefully lets get<N>() count from 0 to N. We can now write a << for tuple:

```
std::ostream& operator << (ostream& os, const tuple<>&) // the empty tuple
{
return os << "{}";
}
```

```
template<typename T0, typename ...T>
ostream& operator<<(ostream& os, const tuple<T0, T...>& t) // an nonempty tuple {
os << ‘{‘ << std::get<0>(t); // print first element print_tuple<1>::print(os,t); // print the rest of the elements return os << ‘}’;
}
```

We can now print a tuple:

```
void user()
{
cout << make_tuple() << ‘\n’;
cout << make_tuple("One meatball!") << ‘\n’; cout << make_tuple(1,1.2,"Tail!") << ‘\n’;
}
```

# 28.7 SI Units Example

Using constexpr and templates, we can compute just about anything at compile time. Providing input for such computations can be tricky, but we can always #include data into the program text. However, I prefer simpler examples that in my opinion stand a better chance when it comes to maintenance. Here, I will show an example that provides a reasonable tradeoff between implementation complexity and utility. The compilation