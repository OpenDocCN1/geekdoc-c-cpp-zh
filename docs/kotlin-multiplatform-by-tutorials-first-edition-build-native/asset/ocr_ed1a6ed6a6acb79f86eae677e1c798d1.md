# _Kotlin Multiplatform by Tutorials_ _Chapter 9: Dependency Injection_

```
```
fatalError("Can't initialize Koin.")
}

//4
private init() {
}

//5
func get<T: AnyObject>() -> T {
    guard let core = core else {
    fatalError("You should call `start()` before using \n
(#function)")
    }

    guard let result = core.get(objCClass: T.self) as? T else {
    fatalError("Koin can't provide an instance of type: \n
(T.self)")
    }

    return result
}
```
```

+   1. Store a reference to the Koin core type. This will make it possible to ask for objects.
+   2. Create a static property for the newly created class to use it as a singleton.
+   3. Call this function when the app starts. Here, you’re calling into Kotlin to initialize Koin. **KoinIOS.shared** is the way Kotlin exposes the **object** you created earlier. If for any reason this procedure fails, you’ll make the app crash.
+   4. Mark the initializer for this class as private. This will prevent people from accidentally initializing the Swift **Koin** class apart from the way you intended.
+   5. This method uses the **get** extension methods you wrote on Koin in Kotlin. It first checks if **core** isn’t **nil**. Then it tries casting from **Any** to the generic type **T**. This will make this function type-safe at the call site.

Two steps remain for using Koin on iOS.

First, open **iOSApp.swift** and start Koin at initialization time.

```
```
@main
struct iOSApp: App {
    init() {
    Koin.start()
    }
    // ...
}
```
```