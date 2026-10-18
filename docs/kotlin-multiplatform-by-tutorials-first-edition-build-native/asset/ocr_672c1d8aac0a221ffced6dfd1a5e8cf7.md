platforms that go way back to the 1990s. Because they are low-level and people don’t use them often, Apple never upgraded them to have a nicer interface. One of them is a C struct called `utsname`. Unix fans, rejoice! Here, you’re calling a C function through Kotlin/Native. How crazy is that? In this block of code, you’re allocating memory using the `memScoped` block and the `alloc()` function call. Then, you pass a pointer to the allocated memory space to the `uname` function, which gets the operating system information and fills it inside `systemInfo`. You then convert the C String filled with the machine name to `NSString` and return it. The cast from `NSString` to Kotlin String is automatic. Phew!

+   4. For getting the CPU type, you can once again dig into C code, or like here, just use the Kotlin/Native `Platform` class.
+   
+   5. You initialize an instance of `ScreenInfo` and store it in `screen` property. As you did on Android, make sure to write the type explicitly.
+   
+   6. The function implementation is basically the same as the Android implementation, except that you’re passing the same string to `NSLog` function.
+   
+   7. You need to combine your knowledge of `UIKit` and `CoreGraphics` to get the screen properties. First, you use the `UIScreen` class to fetch information about the `mainScreen` of the device. Then you use `CGRectGetWidth` and `CGRectGetHeight` functions of `CoreGraphics` to extract width and height from the `nativeBounds` properties, which is a `CGSize` Objective-C struct.

These may look a bit weird for Kotlin and Swift developers. The reason is that you’re using the Objective-C nomenclature for entities. This is how KMP works for Apple platforms. The interoperability is thereby creating a bridge between Kotlin and Objective-C.

The block of code in Section 3 is odd, even for Swift developers. If you were to write this section using Swift, there would also be some travels to the C world:

```
```swift
let deviceModel: String = {
    var systemInfo = utsname()
    uname(&systemInfo)
    let str = withUnsafePointer(to: &systemInfo.machine.0) { ptr in
        return String(cString: ptr)
    }
    return str
}()
```
```

Why Objective-C and not Swift, you may ask. Although Swift interoperability is in the works by KMP creators, they chose to go with Objective-C for a couple of reasons: