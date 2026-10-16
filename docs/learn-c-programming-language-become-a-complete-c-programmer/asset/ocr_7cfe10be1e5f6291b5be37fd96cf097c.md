It would be a good guess that the author of User meant for User::alg() to call User::copy(). However, that’s not what happens. The compiler notices that Index really is a vector defined in std and looks to see if a relevant function is available in std. In <algorithm>, it finds:

```
template<typename In, typename Out>
Out copy(In,In,Out);
```

Obviously, this general template is a perfect match for copy(x,y,false). On the other hand, the copy() in User can be called only with a bool-to-int conversion. For this example, as for equivalent examples, the compiler’s resolution is a surprise to most programmers and a source of very obscure bugs. Using ADL to find fully general templates is arguably a language design error. After all, std::copy() requires a pair of iterators (not just two arguments of the same type, such as the two Indexes). The standard says so, but the code does not. Many such problems can be solved by the use of concepts (§24.3, §24.3.2). For example, had the compiler known that std::copy() required two iterators, a nonobscure error would have been the result.

# Section 26.3.6 Overaggressive ADL 755

```
template<typename In, typename Out> Out copy(In p1, In p2, Out q)
{
static_assert(Input_iterator<In>(), “copy(): In is not an input iterator”);
static_assert(Output_iterator<Out>(), “copy(): Out is not an output iterator”);
static_assert(Assignable<Value_type<Out>,Value_type<In>>(), “copy(): value type mismatch”); // ...
}
```

Better still, the compiler would have noticed that std::copy() wasn’t even a valid candidate for that call and User::copy() would have been invoked. For example (§28.4):

```
template<typename In, typename Out,
typename = enable_if(Input_iterator<In>()
&& Output_iterator<Out>()
&& Assignable<Value_type<Out>,Value_type<In>>())>
Out copy(In p1, In p2, Out q)
{
// ...
}
```

Unfortunately, many such templates are in libraries that a user cannot modify (e.g., the standard library).

It is a good idea to avoid fully general (completely unconstrained) function templates in headers that also contain type definitions, but that’s hard to avoid. If you need one, protecting it with a constraints check is often worthwhile.

What can a user do if a library has trouble-causing unconstrained templates? Often, we know which namespace our function should come from, so we can be specific about that.