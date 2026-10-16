definition of an object. For example:

```
const int model = 90; const int v[] = { 1, 2, 3, 4 }; const int x;
```

```
// model is a const // v[i] is a const
// error : no initializer
```

Because an object declared const cannot be assigned to, it must be initialized. Declaring something const ensures that its value will not change within its scope:

```
void f()
{
model = 200; // error
v[2] = 3; // error
}
```

Note that const modifies a type; it restricts the ways in which an object can be used, rather than specifying how the constant is to be allocated. For example:

```
void g(const X* p)
{
// can’t modify *p here
```

# Section 7.5 Pointers and const 187

```
void h() {
Xval; // valcan be modified here
g(&val);
// ...
}
```

When using a pointer, two objects are involved: the pointer itself and the object pointed to. “Prefixing” a declaration of a pointer with const makes the object, but not the pointer, a constant. To declare a pointer itself, rather than the object pointed to, to be a constant, we use the declarator operator *const instead of plain *. For example:

```
void f1(char* p) {
char s[] = “Gorm”;

const char * pc = s; pc[3] = ‘g’;
pc = p;

// pointer to constant
// error :pc points to constant // OK

char *const cp = s; cp[3] = ‘a’;
cp = p;

// constant pointer // OK
// error :cp is constant

const char *const cpc = s; cpc[3] = ‘a’;
cpc = p;
}
```

```
// const pointer to const
```