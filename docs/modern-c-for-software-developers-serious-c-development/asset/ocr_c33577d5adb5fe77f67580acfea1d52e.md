```
target_compile_options(${PROJECT_NAME}) PRIVATE -fno-omit-frame-pointer
-fsanitize=address
-g3 )
```

```
target_link_libraries(${PROJECT_NAME})
-fsanitize=address
 )
```

The compiler flag g3 sets the amount of debugging information (symbols) that the compiler will insert in the object file(s). g, g1, g2 and g3 are permissible flag values. g3 produces the maximum amount of debugging information.

# Undefined Behavior Sanitizer (UBSan)

The Undefined Behavior Sanitizer (UBSan) is a run-time sanitizer that tests whether an operation has unknown semantics. Some examples of such operations are: divide by zero, out of bounds access of an array, using a null pointer, integer overflow and dangerous narrowing casts. The result of such an operation may cause a segmentation error, return some garbage value or return a seemingly correct value. This type of bug is hard to detect since it may cause a program to crash only sporadically.

UBSan uses a catalogue of predefined undefined error types that it uses to check program expressions.

For GCC and CMake, we enable UBSan with the following syntax in the CMakeLists.txt file:

```
target_compile_options(${PROJECT_NAME}) PRIVATE -fno-omit-frame-pointer
-fsanitize=undefined
-g3 )
```

```
target_link_libraries(${PROJECT_NAME})
-fsanitize=undefined
 )
```