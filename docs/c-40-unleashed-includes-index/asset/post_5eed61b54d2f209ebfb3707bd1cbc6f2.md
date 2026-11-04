
However, as a personal matter of taste, I still find this notation useful for UI programming, prefixing controls with their types. For one thing, the fact that controls are declared in a separate generated code file makes it more difficult to trace back the type of a control when doing code inspections outside an IDE. Furthermore, it's not uncommon to get clashes between control names and local variables. (For example, a seconds value needs to be assigned to a seconds control's Text property.)

Now that looks easy enough, doesn't it? In the Click handler, we first disable all controls to avoid multiple countdowns being active at the same time. Next we create a CountDown instance, casting the NumericUpDown's decimal-typed Value property to uint (something we know will succeed if the NumericUpDown control is configured correctly; that is, with DecimalPlaces set to 0 and its Minimum property set to 0 or more). Two event handlers are created, with help from Visual Studio upon typing +=, which causes the two methods to be generated on the fly. Notice that the explicit delegate instance creation calls can be trimmed away if you find that style clearer:

```csharp
_countDown.Tick += _countDown_Tick;
_countDown.Finished += _countDown_Finished;
```

Code inside the handlers looks reasonable, as well, and should be self-explanatory. As you can guess, there's a little problem lurking around the corner, which is why I'm showing this example. Let's see what the problem is by simply running the program under the debugger by pressing F5. Set the number of seconds to five or so, click Start, and watch what happens. Figure 18.27 shows the result, which might not be quite as expected.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_913_0.png)

FIGURE 18.27 Cross-thread access to UI controls is troublesome.

Can you guess what's going wrong based on the message? Recall how our CountDown is implemented by using a background thread. This was done to prevent the Start call from being blocked. Raising the Tick event ultimately causes method calls to all the subscribed

```csharp
private void btnStart_Click(object sender, EventArgs e) {
    nudSeconds.Enabled = false;
    btnStart.Enabled = false;
}
```

This works like a charm and is permitted because the controls are being touched on the same thread, in particular the so-called UI thread, as where they were created. But in our setting, we're also interacting with controls from another thread (that is, the one that's making our countdown mechanism tick). The observed InvalidOperationException tells us this is a really bad idea.

Luckily, there's an escape valve to deal with this kind of situation, allowing us to run code on the UI thread. In Windows Forms, an Invoke method is provided to do so; in WPF, there's a Dispatcher type that's the central hub for operations that run on the UI thread. Because we're in Windows Forms, let's take a look at this Invoke method:

```csharp
namespace System.Windows.Forms {
    class Control {
        ...
        /// <summary>
        /// Executes the specified delegate on the thread that owns the
        /// control's underlying window handle.
        /// </summary>
        public object Invoke(Delegate method);
        public object Invoke(Delegate method, params object[] args);
        ...
    }
}
```

The summary tells it all, with a few more Win32-specific words like *window handle*, but the important bit is we got our solution to "jump" from the countdown's thread to the UI thread to touch UI controls. And guess what, the argument is of type Delegate, something we've gotten utterly familiar with. The available overload allows for calling a delegate that expects arguments, which get specified through the params array.

Because both Tick and Finished events are raised on the background thread, we need to apply the trick of "thread jumping" in both places:

```csharp
void _countDown_Tick(object sender, TickEventArgs e) {
    this.Invoke(new Action(() => {
        lblTime.Text = string.Format("{0} seconds left", e.Seconds);
    }));
}

void _countDown_Finished(object sender, EventArgs e) {
    this.Invoke(new Action(() => {
        MessageBox.Show("Countdown finished!", this.Text, MessageBoxButtons.OK,
                        MessageBoxIcon.Information);
        _countDown.Tick -= _countDown_Tick;
        _countDown.Finished -= _countDown_Finished;

        lblTime.Text = "";
        nudSeconds.Enabled = true;
        btnStart.Enabled = true;
    }));
}
```

The use of Invoke makes our code work correctly, with the delegates running on the UI thread. Did you see how we've made handy use of a closure in the Tick event handler, to refer to the TickEventArgs object from inside the lambda expression's body?

## THE MYSTERIOUS SYSTEM.DELEGATE TYPE

In the preceding sample, we've seen how the Windows Forms folks typed the argument of the Invoke method as System.Delegate, to allow for every single delegate type. At the time of the first release of Windows Forms, with .NET 1.0, this was very beneficial because no anonymous function expressions, and hence no closures, were present in any of the languages targeting the framework. By supporting any delegate type, users could create a delegate of their taste with the needed number of arguments.

One first mystery is how such a delegate can be invoked by the framework code if the signature of the target method is totally unknown. The answer lies in the CLR's support for reflection again, with support for a DynamicInvoke method on Delegate:

```csharp
/// <summary>
/// Dynamically invokes (late-bound) the method represented by the current
/// delegate.
/// </summary>
public object DynamicInvoke(params object[] args);
```

With that cleared up, you might ask the existential question of whether System.Delegate itself is a delegate type through the eyes of the C# language. Even though it's the base type of all delegates, method group conversions to this type are not permitted. For example:

```csharp
Delegate d = Do;
...
void Do() { /* TODO */ }
```

The first line will fail to compile, resulting in the following message:

```
Cannot convert method group 'Do' to non-delegate type 'System.Delegate'. Did you intend to invoke the method?
```

That answers your question right there. An implication of this rule is that we need to instantiate a delegate object explicitly when passing an argument to Invoke.

> This is just one of the oddities of the type system in the CLR or C# with regard to base types for certain categories of types. As another example, even though System.ValueType is the base type for all value types, it's a reference type by itself.

Finally, we should mention that this common problem of thread affinity has given rise to built-in solutions in the .NET Framework, such as the BackgroundWorker class, which is very useful in cases where an asynchronous operation needs to report through a user interface. Once more, it's event-driven by itself, making it familiar to people who are used to event-based programming already. We cover the BackgroundWorker in Chapter 29, “Threading and Synchronization,” in the section, “BackgroundWorker.”

## Modern Approaches to Reactive Programming

To finish off this chapter, we take a brief look at recent evolutions in the space of reactive, event-based programming. With distributed programs becoming more and more omnipresent, the importance of reactive programming is steadily increasing. Think of technologies such as AJAX, which emphasize the asynchronous nature of communications to prevent keeping the user waiting for a network operation to complete. One of the most typical AJAX examples is a dictionary suggest.

Although the concept of asynchronous distributed computing (a key part of future ways of computing with regard to “the cloud”) is a great way to keep the user interface responsive, it doesn't come for free. Asynchronous programming tends to be hard, especially when events need to be combined somehow. The example shown in Figure 18.29 looks perfectly fine, but there's quite a bit of room for disaster.

Here are a few examples to illustrate the madness we're getting ourselves into by trying to be polite to our users:

- What if the result of querying the dictionary services for re comes back after the result for typing reactive comes back? If this happens, the results of reactive will get overwritten by the results of re. Remember from your networking courses that in-order responses to requests are not a guarantee on the Internet (it's a jungle out there, with packets getting dropped or eaten by evil monsters), so this is not very far-fetched.
- How about a network error that manifests itself during the communication with the dictionary service? Where and how will the error manifest itself as things are happening in an asynchronous manner? How do we hook the event of an error happening in the system to show an error message to the user or to retry the operation?
- Recall the typical difficulties that arise from dealing with asynchronous work in a UI framework context, as shown in Figure 18.27. Can't we make the mandatory “thread jumping” required to update the UI easier to get right?
