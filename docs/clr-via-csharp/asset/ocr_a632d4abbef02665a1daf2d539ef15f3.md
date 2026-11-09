```
```csharp
internal static class RegisteredWaitHandleDemo {
   public static void Main() {
      // Construct an AutoResetEvent (initially false)
      AutoResetEvent are = new AutoResetEvent(false);

      // Tell the thread pool to wait on the AutoResetEvent
      RegisteredWaitHandle rwh = ThreadPool.RegisterWaitForSingleObject(
         are,             // Wait on this AutoResetEvent
         EventOperation,  // When available, call the EventOperation method
         null,            // Pass null to EventOperation
         5000,            // Wait 5 seconds for the event to become true
         false);          // Call EventOperation every time the event is true

      // Start our loop
      Char operation = (Char) 0;
      while (operation != 'Q') {
         Console.WriteLine("S=Signal, Q=Quit?");
         operation = Char.ToUpper(Console.ReadKey(true).KeyChar);
         if (operation == 'S') are.Set(); // User want to set the event
      }

      // Tell the thread pool to stop waiting on the event
      rwh.Unregister(null);
   }

   // This method is called whenever the event is true or
   // when 5 seconds have elapsed since the last callback/timeout
   private static void EventOperation(Object state, Boolean timedOut) {
      Console.WriteLine(timedOut ? "Timeout" : "Event became true");
   }
}
```
```