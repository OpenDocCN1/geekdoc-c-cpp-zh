```
if ((NULL == pp_apple) || (NULL == *pp_apple))
{
/* Handle the NULL pointer error. */
}
```

Fig 9.2 - In this example, short-circuit evaluation is used to ensure correct behaviour of the code rather than to improve performance; because two levels of indirection are used, both pp_apple and *pp_apple must be checked to ensure neither is However, pp_apple must always be checked first, and the second check should only be performed if it is not Although this is valid C, it is still not ideal – a programmer unaccustomed with short-circuit evaluation will not realise that the second check is performed only when the first fails.

# Optimising keywords

The C language includes some keywords which can aid optimisation. Strictly speaking, the keywords themselves do not usually cause any optimisation to take place; rather, they serve as hints to the compiler as to where optimisation might be possible. The compiler may choose not to perform the optimisation or, conversely, to perform the optimisation even if the keyword was not used.

The dubiously named const keyword is one which you should be familiar with and use wherever possible. Despite the name, a variable declared const is not necessarily constant (a true constant has a value which can be known at compile time); rather, it is better described as being although even this may not be considered entirely Whether the name is accurate or