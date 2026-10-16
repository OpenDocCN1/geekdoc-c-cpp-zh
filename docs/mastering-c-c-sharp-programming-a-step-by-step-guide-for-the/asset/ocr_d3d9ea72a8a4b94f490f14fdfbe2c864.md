```
```csharp
{
	static void Main() {
		unsafe {
			int* values = stackalloc int[20];
			int* p = &values[1];
			int* q = &values[15];
			Console.WriteLine("p - q = {0}", p - q);
			Console.WriteLine("q - p = {0}", q - p);
		}
	}
}
```
```

p - q = -14
q - p = 14

If an operation of pointer arithmetic overflows the pointer type domain, the result will always be truncated in a similar fashion to implementation-defined but there will be no exceptions thrown.

# Pointer Comparison

+   - bool operator ==(void* x, void* y);
+   - bool operator !=(void* x, void* y);
+   - bool operator <(void* x, void* y);
+   - bool operator >(void* x, void* y);
+   - bool operator <=(void* x, void* y);
+   - bool operator >=(void* x, void* y);