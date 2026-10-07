# 29. De-template-ize Your Generic Code

Move things outside of your templates when you can. Use other functions. Use base classes. The compiler is still to inline them or leave them out of line.

De-template-ization will improve compile times and reduce binary sizes. Both are helpful. IMO is still free to inline or leave them out of line. It also eliminates the thing that people think of as “template code bloat” (which IMO [doesn't exist'](https://articles.emptycrate.com/2008/05/06/nobody_understands_c_part_5_template_code_bloat.html)) (article formatting got broken at some point, sorry).

A new lambda for each function instantiation.

```
template<typename T>
void do_things()
{
    // this lambda must be generated for each
    // template instantiation
    auto lambda = [](){/* some lambda that doesn't capture */ };
    auto value = lambda();
}
```

Compared to:

> https://articles.emptycrate.com/2008/05/06/nobody_understands_c_part_5_template_code_bloat.html