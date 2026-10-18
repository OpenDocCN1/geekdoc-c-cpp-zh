By adding a simple `get()` call, you can silence the errors of Android Studio. However, you shouldn’t forget to provide an instance of `DatabaseHelper` through Koin.

Since database is one of the core functionalities of the app, add a module to the `core` property inside the `Modules` object:

```
```kotlin
val core = module {
    factory { Platform() }
    factory { DatabaseHelper(get()) }
}
```
```

A single dependency remains to be declared — the `SqlDriver`, which `DatabaseHelper` needs. Since `SqlDriver` is platform-dependent, you can declare it inside the `platformModule` you already defined through the expect/actual mechanism.

# Android

Open **KoinAndroid.kt** and add a singleton definition underneath the `Settings` declaration as follows:

```
```kotlin
single<SqlDriver> {
    AndroidSqliteDriver(OrganizeDb.Schema, get(), "OrganizeDb")
}
```
```

Creating an instance of `AndroidSqliteDriver` requires at least a database scheme, which you’ll get from the generated `OrganizeDb` class, and an instance of `Context`, which you get through Koin by taking advantage of the `get()` function. Optionally, you could specify a name.

Build and run the app, add a few reminders and check some of them off the list. Then kill the app and launch it again. Everything is there because it should have always been this way.

# iOS

Open **KoinIOS.kt** and set this as the `platformModule` actual property:

```
```kotlin
actual val platformModule: Module = module {
    single<SqlDriver> {
        NativeSqliteDriver(OrganizeDb.Schema, "OrganizeDb")
    }
}
```
```