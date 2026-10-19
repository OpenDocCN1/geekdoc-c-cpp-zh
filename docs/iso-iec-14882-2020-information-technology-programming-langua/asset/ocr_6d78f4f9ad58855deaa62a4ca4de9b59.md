+   - 0, if the next n or fewer bytes complete the multibyte character that corresponds to the U+0000 Unicode character (which is the value stored).
+   - between 1 and n (inclusive), if the next n or fewer bytes complete a valid multibyte character (which is the value stored); the value returned is the number of bytes that complete the multibyte character.
+   - (size_t)(-3), if the next character resulting from a previous call has been stored (no bytes from the input have been consumed by this call).
+   - (size_t)(-2), if the next n bytes contribute to an incomplete (but potentially valid) multibyte character, and all n bytes have been processed (no value is stored).
+   - (size_t)(-1), if an encoding error occurs, in which case the next n or fewer bytes do not contribute to a complete and valid multibyte character (no value is stored); the value of the macro EILSEQ is stored in errno, and the conversion state is unspecified.

```
size_t c8rtomb(char* s, char8_t c8, mbstate_t* ps);
```

Effects: If s is a null pointer, equivalent to c8rtomb(buf, u8'\0', ps) where buf is an internal buffer. Otherwise, if c8 completes a sequence of valid UTF-8 code units, determines the number of bytes needed to represent the multibyte character (including any shift sequences), and stores the multibyte character representation in the array whose first element is pointed to by s. At most MB_CUR_MAX bytes are stored. If the multibyte character is a null character, a null byte is stored, preceded by any shift sequence needed to restore the initial shift state; the resulting state described is the initial conversion state.

Returns: The number of bytes stored in the array object (including any shift sequences). If c8 does not contribute to a sequence of char8_t corresponding to a valid multibyte character, the value of the macro EILSEQ is stored in errno, (size_t)(-1) is returned, and the conversion state is unspecified.

Remarks: Calls to c8rtomb with a null pointer argument for s may introduce a data race (16.4.6.10) with other calls to c8rtomb with a null pointer argument for s.