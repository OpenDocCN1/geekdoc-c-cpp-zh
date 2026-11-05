# Why it’s useful:

It automatically recompiles and reruns your project when changes are saved.

Perfect for Console Apps, APIs, or Blazor development.

Saves time and avoids the boring manual stop-run cycle.

# How it works:

Watches for changes in .cs files (and other relevant files).

Triggers a rebuild and relaunches the app.

Works with run, test, build, etc. Example:

dotnet watch test reruns your tests on every file change.

# When to use:

During development of apps where instant feedback helps.

When tweaking small bits of logic frequently.

# [Supplement]

dotnet watch can be configured using a watch section in your project’s .csproj file to ignore or include certain files.

It internally uses file system watchers to detect changes efficiently.

You can pass arguments too:

```
```text
dotnet watch run——my-arg value
```
```