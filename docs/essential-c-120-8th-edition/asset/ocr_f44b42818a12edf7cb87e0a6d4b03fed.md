# Chapter 20: Programming the Task-Based Asynchronous Pattern

.Unwrap()
.ContinueWith(antecedent) =>

```
int textOccurrenceCount = antecedent.Result;
Console.WriteLine(
  $"{Environment.NewLine}{findText}' appears \{textOccurrenceCount} times at URL '{url}';
n
try {
  while (!task.Wait(100)) {
    Console.Write(".*");
  }
} catch (AggregateException exception) {
  exception.Flatten();
  try {
    exception.Handle(innerException => {
      // Rethrowing rather than using
      // if condition on the type
      ExceptionDispatchInfo.Capture(innerException)
      .Throw();
      return true;
    });
  } catch (HttpRequestException) {
    // ...
  } catch (IOException) {
    // ...
  }
}
```

```
private static async Task<int> CountOccurrencesAsync(byte[] downloadData, string findText) {
```