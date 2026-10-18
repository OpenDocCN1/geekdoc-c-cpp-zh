4. `kotlin.test` library includes several **assert** functions, which you can take advantage of. Here, you’re using `assertTrue` to check if `count` equals 1. If that’s true, it means the creation process was successful. If not, you show a message in the console.

The `reminders` property in **RemindersViewModel** was `private` when you wrote it. Since **commonTest** is in the same module as **commonMain**, you can change the visibility modifier for that property to `internal`. This way, outsiders using the **shared** module such as **androidApp** and **iosApp** won’t see any changes and the property would be visible to your test functions.

Open **RemindersViewModel.kt** and change the aforementioned property to this:

```
internal val reminders: List<Reminder>
    get() = repository.reminders
```

Now it’s time to run the test. To run the tests on all platforms at once, you can try either of these actions:

+   - Choose **allTests** from the list of tasks in Gradle pane in Android Studio.

![](bbox=[0.214, 0.483, 0.786, 0.838])

*Fig. 8.6 - Choosing allTests from Gradle pane*

+   - Run the command `./gradlew :shared:allTests` in Terminal while you’re in the working directory of the project.