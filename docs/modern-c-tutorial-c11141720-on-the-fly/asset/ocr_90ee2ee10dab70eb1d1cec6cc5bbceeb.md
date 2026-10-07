# 5.4 std::weak_ptr CHAPTER 05 SMART POINTERS AND MEMORY MANAGEMENT

![](bbox=[0.233, 0.087, 0.766, 0.246])

```
-B() {
  std::cout << "B was destroyed" << std::endl;
}
int main() {
  std::shared_ptr<A> a = std::make_shared<A>();
  std::shared_ptr<B> b = std::make_shared<B>();
  a->pointer = b;
  b->pointer = a;

  return 0;
}
```

The result is that A and B will not be destroyed. This is because the pointer inside a, b also references a, b, which makes the reference count of a, b become 2, leaving the scope. When the a, b smart pointer is destroyed, it can only cause the reference count of this area to be decremented by one. This causes the memory reference count pointed to the a, b object to be non-zero, but the external has no way to find this, and also caused a memory leak, as shown in Figure 5.1.

The solution to this problem is to use the weak reference std::weak_ptr, which is a weak reference (compared to std::shared_ptr is a strong reference). A weak reference does not cause an increase in reference count. When a weak reference is used, the final release process is shown in Figure 5.2.

In the above figure, B is left in the last step, and B does not have any smart pointers to it, this memory resource will also be released.

std::weak_ptr has no * and -> operator, so it can't operate on resources. Its only function is to check if std::shared_ptr exists, expired() method can return false when the resource is not released, otherwise it returns true.