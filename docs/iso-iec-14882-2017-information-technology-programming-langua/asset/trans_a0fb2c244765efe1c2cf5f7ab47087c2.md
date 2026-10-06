

## ISO/IEC 14882:2017(E)

```cpp
template <class T> struct is_array;
template <class T> struct is_pointer;
template <class T> struct is_lvalue_reference;
template <class T> struct is_rvalue_reference;
template <class T> struct is_member_object_pointer;
template <class T> struct is_member_function_pointer;
template <class T> struct is_enum;
template <class T> struct is_union;
template <class T> struct is_class;
template <class T> struct is_function;
```

```cpp
// 23.15.4.3. 复合类型分类
template <class T> struct is_reference;
template <class T> struct is_arithmetic;
template <class T> struct is_fundamental;
template <class T> struct is_object;
template <class T> struct is_scalar;
template <class T> struct is_compound;
template <class T> struct is_member_pointer;
```

```cpp
// 23.15.4.4. 类型属性
template <class T> struct is_const;
template <class T> struct is_volatile;
template <class T> struct is_trivial;
template <class T> struct is_trivially_copyable;
template <class T> struct is_standard_layout;
template <class T> struct is_pod;
template <class T> struct is_empty;
template <class T> struct is_polymorphic;
template <class T> struct is_abstract;
template <class T> struct is_final;
template <class T> struct is_aggregate;
```

```cpp
template <class T> struct is_signed;
template <class T> struct is_default_constructible;
template <class T> struct is_copy_constructible;
template <class T> struct is_move_constructible;
```

```cpp
template <class T, U> struct is_swappable_with;
template <class T, U> struct is_swappable;
```

```cpp
template <class T> struct is_destructible;
```

```cpp
template <class T, class... Argo> struct is_trivially_constructible;
template <class T> struct is_trivially_default_constructible;
template <class T> struct is_trivially_copy_constructible;
template <class T> struct is_trivially_move_constructible;
```

```cpp
template <class T, class U> struct is_trivially_assignable;
template <class T> struct is_trivially_copy_assignable;
template <class T> struct is_trivially_move_assignable;
template <class T> struct is_trivially_destructible;
```

```cpp
template <class T, class...> Arg2 struct is_not_row_constructible;
template <class T> struct is_not_row_default_constructible;
template <class T> struct is_not_row_copy_constructible;
template <class T> struct is_not_row_move_constructible;
```

```cpp
template <class T, class U> struct is_not_row_assignable;
template <class T> struct is_not_row_copy_assignable;
template <class T> struct is_not_row_move_assignable;
```

```cpp
template <class T, class U> struct is_not_row_swappable_with;
template <class T> struct is_not_row_swappable;
```

```cpp
template <class T> struct is_not_row_destructible;
template <class T> struct has_virtual;
template <class T> struct has_representations;
// 23.15.5. 类型查询
template <class T> struct alignment_of;
template <class T> struct rank;
template <class T> unsigned I =
```
```cpp
// 23.15.6. 类型关系
template <class T, U> struct is_same;
template <class Base, Derived> struct is_base;
template <class From, To> struct is_convertible;
```cpp
template <class T, class...> struct is_not_invocable;
template <class T, class U> struct is_not_invocable_r;
// 23.15.7. const/volatile 修改
template <class T> struct remove_const;
template <class T> struct remove_volatile;
template <class T> struct remove_cv;
template <class T> struct add_const;
template <class T> struct add_volatile;
template <class T> struct add_cv;
```cpp
template <class T> using remove_const_t = typename remove_const<T>::type;
template <class T> using remove_volatile_t = typename remove_volatile<T>::type;
template <class T> using remove_cv_t = typename remove_cv<T>::type;
template <class T> using add_const_t = typename add_const<T>::type;
template <class T> using add_volatile_t = typename add_volatile<T>::type;
template <class T> using add_cv_t = typename add_cv<T>::type;
```
// 23.15.7.2. 引用修改
template <class T> struct remove_reference;
template <class T> struct add_lvalue_reference;
template <class T> struct add_rvalue_reference;
```cpp
template <class T> using remove_reference_t = typename remove_reference<T>::type;
template <class T> using add_lvalue_reference_t = typename add_lvalue_reference<T>::type;
template <class T> using add_rvalue_reference_t = typename add_rvalue_reference<T>::type;
```
// 23.15.7.3. 符号修改
template <class T> struct make_signed;
template <class T> struct make_unsigned;
```cpp
template <class T> using make_signed_t = typename make_signed<T>::type;
template <class T> using make_unsigned_t = typename make_unsigned<T>::type;
```
// 23.15.7.4. 数组修改
template <class T> struct remove_extent;
template <class T> struct remove_all_extents;
```cpp
template <class T> using remove_extent_t = typename remove_extent<T>::type;
template <class T> using remove_all_extents_t = typename remove_all_extents<T>::type;
```
// 23.15.7.5. 指针修改
template <class T> struct remove_pointer;
template <class T> struct add_pointer;
```cpp
template <class T> using remove_pointer_t = typename remove_pointer<T>::type;
template <class T> using add_pointer_t = typename add_pointer<T>::type;
```
```cpp
// 23.15.6. 其他转换
template <class T, size_t Len> struct aligned_storage;
template <typename...> struct union;
template <class T> struct decay;
template <class bool, T> struct enable_if;
template <class bool, T> struct conditional;
template <class T...> struct common_type;
template <typename T> struct underlying_type;
template <class Fn, class...> struct invoke_result;
template <class T...> struct void_t;
```

// 23.15.8. 逻辑运算符属性
template <class B> struct conjunction;
template <class B> struct disjunction;
template <class B> struct negation;

// 23.15.9. 原生类型分类
template <class T> inline constexpr bool is_void_v = is_void<T>::value;
template <class T> inline constexpr bool is_null_pointer_v = is_null_pointer<T>::value;
template <class T> inline constexpr bool is_integral_v = is_integral<T>::value;
template <class T> inline constexpr bool is_floating_point_v = is_floating_point<T>::value;
template <class T> inline constexpr bool is_array_v = is_array<T>::value;
template <class T> inline constexpr bool is_pointer_v = is_pointer<T>::value;
template <class T> inline constexpr bool is_lvalue_reference_v = is_lvalue_reference<T>::value;
template <class T> inline constexpr bool is_rvalue_reference_v = is_rvalue_reference<T>::value;

