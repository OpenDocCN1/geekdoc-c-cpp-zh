```
```kotlin
public fun openLink(url: String)
}
```
```

This is the object the UI will call.

Alternatively, you can just define the `openLink` function without adding it to an `object`:

```
```kotlin
public expect fun openLink(url: String)
```
```

You can call this function directly from **androidApp** and **desktopApp**, since you reference it directly. However, from **iosApp**, you would need to access it via:

```
```kotlin
PlatformActionKt.openLink(url: "\\(item.link)")
```
```

Since there’s no class defined, the compiler creates one when generating the framework and uses the class name plus the extension of the file as its name.

Although you could define a different name, you’re always going to have the **kt** prefix — which isn’t the most sympathetic name, especially when you’re trying to convince the iOS team to adopt a shared module written in Kotlin. :-]

Android Studio prompts a suggestion to automatically generate the missing files. Ignore it for now. In some IDE versions, this feature is not working as expected and ends up creating the files in wrong directories. To avoid any unexpected error, you’re going to add all of these files manually.

Create a **PlatformAction.kt** file for **androidMain**, **iosMain** and **desktopMain**. They should all be in the same directory for each of the platforms: **com.raywenderlich.learn.action.**

Define an empty `actual` function:

```
```kotlin
public actual object Action {

  public actual fun openLink(url: String) {}
}
```
```

Implement the `openLink` functions for the different targets:

+   - **androidApp**: Open the **MainActivity.kt** file and scroll until you see an `openEntry` function. Copy its content and paste it on the `openLink` function you created in **shared-action/androidMain**:

```
```kotlin
public actual fun openLink(url: String) {
```
```