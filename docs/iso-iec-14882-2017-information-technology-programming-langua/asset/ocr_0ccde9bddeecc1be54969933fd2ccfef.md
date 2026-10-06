# ISO/IEC 14882:2017(E)

```
using state_type = typename Codecvt::state_type;
The type shall be a synonym for Codecvt::state_type.
explicit wbuffer_convert(
streambuf* bytebuf = nullptr,
nCodecvt* pcvt = new Codecvt,
state_type state = state_type());
```

Requires: pcvt != nullptr.
Effects: The constructor constructs a stream buffer object, initializes bufptr to bytebuf, initializes cvptr to pcvt, and initializes cvtstate to state.

```
-wbuffer_convert();
Effects: The destructor shall delete cvptr.
```