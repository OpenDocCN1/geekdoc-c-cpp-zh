# Returning Objects via Pointer Arguments

```
weak id weak;
int writeBack(id *aValue) {
    *aValue = [NSObject new];
    weak = *aValue;
    return 0;
}

int main(void) {
    @autoreleasepool {
        id object;
        writeBack(&object);
        NSLog("Object: %@", object);
        object = nil;
        NSLog("Object: %@", weak);
    }
    return 0;
}
```

From: writeback.m

In ARC mode, pointer-to-pointer arguments are somewhat complicated. These are typically used for two things, either passing arrays or returning objects. If you are passing an array down the stack, you should make sure that you declare it as const. This tells the compiler that the callee will not perform any assignments to it, so ARC can pass the array without any complex interaction.