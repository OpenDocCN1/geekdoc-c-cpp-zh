# Categories of Types

the location in memory that contains the data, an operation known as dereferencing. The memory area of the data reference type points to is called the heap (see Figure 3.2).

![](bbox=[0.213, 0.206, 0.545, 0.693])

FIGURE 3.2: Reference types point to the heap

A reference type does not require the memory copy of the data that a value type does, which makes copying reference types more efficient than copying large value types. When assigning the value of one reference type variable to another reference type variable, only the reference is copied, not the data referred to. In practice, a reference is always the same size as the “native size” of the processor—a