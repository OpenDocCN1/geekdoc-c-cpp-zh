
## Kotlin Multiplatform by Tutorials Chapter 8: Testing

Create a new test function and put the cursor in the empty body.

```swift
func testOpeningAndClosingAboutPage() {
    // Put the cursor here
}
```

At the bottom of the page, a **Record** button would appear. Click on it. The app will run on the simulator, and Xcode will turn whatever action you do in the app into code.

![](img/2f50555a40af4ea8c85f09e577f0c5b9_188_0.png)

Fig. 8.11 - Xcode UI Test Record button

Do these actions in order:

1. Tap the **About** button.
2. When the **About** page comes up, tap the **Done** button.
3. Stop recording using the same button with which you started recording.

Take a look at the test function. Xcode has added code for you. It will be something like this.

```swift
func testOpeningAndClosingAboutPage() {
    let app = XCUIApplication()
    app.toolbars["Toolbar"].buttons["aboutButton"].tap()
    app.navigationBars["About Device"].buttons["Done"].tap()
}
```

If that’s all you had in mind, you’re good to go! Otherwise, this gives you a starting point for writing your tests. You can also learn from this feature how to find elements on screen and act on them.

Another thing to take note of is that Xcode automatically goes for the `accessibilityIdentifier` if you’d set any. If not, it uses the static title to query elements. It’s a great practice to always set this modifier on elements.

That said, you can take cues from Xcode’s automatic test recording system and have this test function:

```swift
func testOpeningAndClosingAboutPage() {
    // 1
    app.buttons["aboutButton"].tap()

    // 2
    let aboutPageTitle = app.staticTexts["About Device"]
    XCTAssertTrue(aboutPageTitle.exists)

    // 3
    app.navigationBars["About Device"].buttons["Done"].tap()

    // 4
    let remindersPageTitle = app.staticTexts["Reminders"]
    XCTAssertTrue(remindersPageTitle.exists)
}
```

1. Simulate tapping the About button when the app launches.
2. Check if there’s a text on screen with About Device content. The About page has this title, and it’s only there if that page is onscreen.
3. Find the Done button in one of the app’s navigation bars with an About Device title and try tapping on it.
4. When you close the About page, the app should be in the Reminders page. Check for the page title if this is the case.

Run all the tests in iosAppUITests class by putting your cursor in the middle of its name and pressing Command-U.

Browse through the results in the Xcode console, or see the green checkmarks in the code gutter and the Test Navigator and rejoice!

![](img/2f50555a40af4ea8c85f09e577f0c5b9_189_0.png)

![](img/2f50555a40af4ea8c85f09e577f0c5b9_190_0.png)

Fig. 8.13 - Xcode UI Test Success - Gutter

### Challenge

Here is a challenge for you to see if you’ve got the idea. The solution is inside the materials for this chapter.

### Challenge: Writing tests for RemindersRepository

Going one level deeper into the app’s architectural monument, it’s essential to have a bulletproof repository. After all, repositories are the backbone of the viewModels in **Organize**. Although it may seem effortless and similar to the viewModels for the time being, you’ll see how these tests will play a vital role when you connect a database to the repository as you move forward.

With this explanation in mind, try to create a test suite for `RemindersRepository`.

### Key points

- KMP will help you write less test code in the same way that it helped you write less business logic code.
- You can write tests for your common code as well as for platform-specific code — all in Kotlin.
- Declaring dependencies to a testing library for each platform is necessary. KMP will run your tests via the provided environment — such as JUnit on JVM.
- Using expect/actual mechanisms in test codes is possible.
- For UI tests, you consult each platform’s provided solution: Jetpack Compose Tests for UIs created with Jetpack Compose and XCTest for UIs created with UIKit or SwiftUI.

### Where to go from here?

This chapter barely scratched the surface of testing. It didn’t talk about mocks and stubs, and it tried not to use third-party libraries, for that matter. There are a few libraries worth mentioning, though:

- **Kotest**: A multiplatform Kotlin testing library with extended assertions and support for property testing. It can generate values for edge cases and random values.
- **Turbine**: A small multiplatform library geared toward testing Kotlin Flows. This chapter didn’t talk about Coroutines and Flows. However, if you ever wanted to test those, take a look at Turbine as `kotlinx-coroutines-test` library doesn’t support Kotlin/Native yet.
- **MockK**: This is the most famous library for mocking in Kotlin. Although there’s a multiplatform version available, it lacks support for iOS.

If you want to learn more about testing in general, there are great resources out there, such as screencasts and articles, as well as these two books from raywenderlich.com:

- Android Test-Driven Development by Tutorials
- iOS Test-Driven Development by Tutorials

## 9 Dependency Injection

Written by Saeed Taheri

Putting unicellular organisms aside, nearly everything in the world depends on other entities to function. Whether it’s something in nature or something mankind has created, it usually takes multiple things to create a working instance of anything.

Imagine an assembly line in a car factory. They don’t create the engines and the wheels on the assembly line. Car manufacturers outsource many of the parts to other companies. In the end, they bring them all to the assembly line, _inject_ each part into the making-in-progress and a shiny new car appears. The car is _dependent_ on other objects. The same applies to the software world.

If you were to model the `Car` into a class, one of its dependencies would be the `Engine`. The car object shouldn’t be responsible for creating the engine. You should inject the engine from outside into the assembly line — or in programming nomenclature, constructor, or initializer.

### Advantages of dependency injection

Dependency injection, or DI, has many advantages.

- **Maintainability:** DI makes your code maintainable. If your classes are loosely coupled, you can catch bugs more easily and address a possible issue faster than you would with a convoluted class that doesn’t adhere to the single-responsibility principle.
- **Reusability:** Going back to the car factory example, you’re able to reuse the same model of wheels for many cars the factory manufactures. Loosely coupled code will let you reuse many parts of your code in different ways.
- **Ease of refactoring:** There may come a time in the lifetime of your app when you need to apply a change to your codebase. The less coupled your classes are, the easier the process will be. Imagine you needed to change the engine if you wanted to have new headlights!
- **Testability:** Everything comes back to the code being loosely coupled. If each object is self-contained, you can test its functionality independent of others. No one would like a car whose engine wouldn’t work when a windshield wiper is broken! This way, each team responsible for each module will test their product and hand it over to other teams.

You should go to each of these files and provide an instance of `RemindersRepository`. What if the repository has its own dependencies? And what if those dependencies have their dependencies as well? This is a rabbit hole you want to avoid getting into!

You can provide all the dependencies yourself and no one can prevent you from doing so. Off the record, iOS developers usually do all this and write all the boilerplates by themselves, since there’s not a popular library or methodology which everyone agrees on.

However, in the Android world, some libraries that solve this problem by automating the process of creating and providing dependencies. They fall into two categories:

- Static solutions, which generate the dependency graph at compile time.
- Solutions that connect the dependencies at runtime.

The most famous library for the first category is Dagger. Recently, Google introduced Hilt, which they built on top of the foundations of Dagger. Google recommends Hilt as part of their app architecture suggestions.

The catch is that neither Dagger nor Hilt is available for KMP. Thus, the approach you can take is to do manual DI or use the most famous library of the second category: Koin.

Many would call libraries like Koin — which resolve dependencies at runtime — Service Locators. Those who favor static DI libraries will seriously object if you call Koin a DI library. However, here you’re free to call it whatever you like.

### Setting up Koin

Setting up Koin is similar to how you’ve set up other multiplatform libraries in the previous chapters - a shared part and some specific libraries to use for each platform.

Open `build.gradle.kts` for the project and add a top-level constant for the Koin version. As of writing, the latest version of Koin is 3.1.5.

```kotlin
val koinVersion by extra("3.1.5")
```

Next, open `build.gradle.kts` for the shared module.

Add a dependency for commonMain source set as follows:
