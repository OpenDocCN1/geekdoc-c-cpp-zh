a union. The former method is potentially undefined behaviour, except when the object address is cast to a pointer to a converting from a pointer to char to another pointer type, however, can still result in undefined behaviour – the requirement given in the C Standard is, when casting pointers, the types pointed to must have compatible alignment in memory.

Note that even if two types are the same size, the rules governing their alignment in memory may still differ and casting from one to the other may still cause problems. The latter method of using a union is sometimes mistakenly believed to be allowed by the C Standard, but this is not strictly true; it is implementation defined behaviour in C89 and unspecified behaviour C99 and Type punning should only ever be undertaken with the greatest care; it is important to document any assumptions made in doing so and to use preprocessor directives or other available methods to enforce them wherever possible.

```
/* Read a (signed) 32-bit word from an array of
 * bytes. */
int32_t int32_from_bytes(uint8_t * p_bytes)
{
/* Cast p_bytes to a pointer to an int32 then
 * dereference and return. */
return *((int32_t *) p_bytes);
}
```

Fig 5.2a

```
/* Make a float from an array of packed
 * bytes. */
float float_from_bytes(uint8_t * p_bytes)
```