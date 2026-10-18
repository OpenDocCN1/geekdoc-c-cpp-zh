mechanism. It’s already there in the starter project. Take a look at its implementation if you’re interested.

Next, add a function to update the `isCompleted` status of a reminder:

```
```
fun markReminder(id: String, isCompleted: Boolean) {
    val index = _reminders.indexOfFirst { it.id == id }
    if (index != -1) {
        _reminders[index] = _reminders[index].copy(isCompleted = isCompleted)
    }
}
```
```

It first checks if an item with the `id` exists. If the answer is yes, it updates the `isCompleted` value.

In the end, create a public getter property for all the reminders. Later, you’ll change this to a Kotlin Flow to be able to propagate live changes to the viewmodel and view. Since using Flows on iOS is a bit tricky, you’ll stick to plain properties for now.

```
```
val reminders: List<Reminder>
    get() = _reminders
```
```

You created a nice-looking API for the repository. Good job!

# ## Creating RemindersViewModel

Inside the **presentation** directory of **commonMain** module, create a new file and name it **RemindersViewModel.kt**. Update it with the following:

```
```
class RemindersViewModel : BaseViewModel() {
    //1
    private val repository = RemindersRepository()

    //2
    private val reminders: List<Reminder>
    get() = repository.reminders

    //3
    var onRemindersUpdated: ((List<Reminder>) -> Unit)? = null
    set(value) {
        field = value
        onRemindersUpdated?.invoke(reminders)
    }

    //4
    fun createReminder(title: String) {
        val trimmed = title.trim()
        if (trimmed.isNotEmpty()) {
            repository.createReminder(title = trimmed)
        }
    }
}
```
```