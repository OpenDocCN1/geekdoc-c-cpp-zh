
# 示例

## Example 1

```cpp
auto f() { // OK: return type is void
auto g() { // error: cannot deduce auto* from void()
```

## Example 2

```cpp
auto f() { // OK: return type is void
auto g() { // error: cannot deduce auto* from void()
```

## Example 3

```cpp
auto f() { // OK: return type is void

auto g() { // error: cannot deduce auto* from void()
```

## Example 4

```cpp
auto f() { // OK: return type is void
auto g() { // error: cannot deduce auto* from void()
```

## Example 5

```cpp
auto f() { // OK: return type is void
auto g() { // error: cannot deduce auto* from void()
```

## Example 6

```cpp
auto f() { // OK: return type is void
auto g() { // error: cannot deduce auto* from void()
```

## Example 7

```cpp
auto f() { // OK: return type is void
auto g() { // error: cannot deduce auto* from void()
```

```cpp
struct A {
  int a;
};
```

```cpp
decltype<auto> double(); // OK
```
