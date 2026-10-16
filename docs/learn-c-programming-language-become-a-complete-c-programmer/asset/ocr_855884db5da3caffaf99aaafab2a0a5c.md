use_facet() might throw bad_cast (§39.3.1). The behavior of a << for a built-in type, such as double, is defined by the C++ standard. Consequently, the question is not what handle_ioexception() should do but rather how it should do what the standard prescribes. If badbit is set in this ostream’s exception state (§38.3), the exception is simply re-thrown. Otherwise, an exception is handled by setting the stream state and continuing. In either case, badbit must be set in the stream state (§38.4.5.1):

```
template<class C, class Tr>
void handle_ioexception(basic_ostream<C,Tr>& s)// called from catch-clause
{
if (s.exceptions()&ios_base::badbit) { try {
s.setstate(ios_base::badbit); // might throwbasic_ios::failure
}
catch(...) {
// ... do nothing ...
}
throw; // re-throw
}
s.setstate(ios_base::badbit);
}
```

The try-block is needed because setstate() might throw basic_ios::failure (§38.3, §38.4.5.1). However,if badbit is set in the exception state, operator<<( ) must re-throw the exception that caused handle_ioexception() to be called (rather than simply throwing basic_ios::failure).

The << for a built-in type, such as double, must be implemented by writing directly to a stream buffer. When writing a << for a user-defined type, we can often avoid the resulting complexity by expressing the output of the user-defined type in terms of output of existing types (§39.3.2).

# Section 39.4.2.3 Numeric Input 1133

# 39.4.2.3 Numeric Input

When reading from a stream buffer (§38.6), an istream relies on the num_get facet:

num_get<In = istreambuf_iterator<C>> facet (§iso.22.4.2.1)

Read [b:e) into v, using formatting rules from s, reporting errors by setting r

```
In get(In b, In e, ios_base& s, ios_base::iostate& r, bool& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, long& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, long long& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, unsigned short& v) const; In get(In b, In e, ios_base& s, ios_base::iostate& r, unsigned int& v) const; In get(In b, In e, ios_base& s, ios_base::iostate& r, unsigned long& v) const; In get(In b, In e, ios_base& s, ios_base::iostate& r, unsigned long long& v) const; In get(In b, In e, ios_base& s, ios_base::iostate& r, float& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, double& v) const;
```