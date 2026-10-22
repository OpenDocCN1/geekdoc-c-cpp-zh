isDefaultConstructible can be used as follows:
    isDefaultConstructible(type<int>)  // true (int is default-constructible)
    isDefaultConstructible(type<int&>) // false (references are not default-constructible)