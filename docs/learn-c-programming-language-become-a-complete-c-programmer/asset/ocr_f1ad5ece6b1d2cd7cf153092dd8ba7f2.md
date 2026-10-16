```
"winter"
};
```

Then, we override the Season_io functions that convert between the string representation and the enumerators:

```
const string& US_season_io::to_str(Season x) const
{
if (x<spring || winter<x) {
static const string ss = "no-such-season"; return ss;
}
return seasons[x];
}
bool US_season_io::from_str(const string& s, Season& x) const {
const string*p= find(begin(seasons),end(seasons),s); if (p==end)
return false;
x = Season(p-begin(seasons));
return true;
}
```

Note that because US_season_io is simply an implementation of the Season_io interface, I did not define an id for US_season_io. In fact, if we want US_season_io to be used as a Season_io, we must not give US_season_io its own id. Operations on locales, such as has_facet (§39.3.1), rely on facets implementing the same concepts being identified by the same id (§39.3).

The only interesting implementation question is what to do if asked to output an invalid Season. Naturally, that shouldn’t happen. However, it is not uncommon to find an invalid value for a simple user-defined type, so it is realistic to take that possibility into account. I could have thrown an exception, but when dealing with simple output intended for humans to read, it is often helpful to produce an “out-of-range” representation for an out-of-range value. Note that for input, the errorhandling policy is left to the >> operator, whereas for output, the facet function to_str() implements an error-handling policy. This was done to illustrate the design alternatives. In a “production design,” the facet functions would either implement error handling for both input and output or just report errors for >> and << to handle.

This Season_io design relies on derived classes to supply the locale-specific strings. An alternative design would have Season_io itself retrieve those strings from a locale-specific repository (see §39.4.7). The possibility of having a single Season_io class to which the season strings are passed as constructor arguments is left as an exercise.

# 39.3.3 Uses of locales and facets

The primary use of locales within the standard library is in I/O streams. However, the locale mechanism is a general and extensible mechanism for representing culture-sensitive information. The messages facet (§39.4.7) is an example of a facet that has nothing to do