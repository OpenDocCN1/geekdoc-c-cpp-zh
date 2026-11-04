The delegates used to define the events look like this:

```
delegate void MouseEventHandler(object sender, MouseEventArgs e);
delegate void KeyPressEventHandler(object sender, KeyPressEventArgs e);
```

While having specialized knowledge about the events that occurred through their arguments (for example, the mouse cursor position at the time of the click), we might just be interested in the mere fact that any of those events happened without requiring additional context. In other words, we want to write the following:

```
txtAmount.KeyPress += this.LoggingHandler;
btnSave.MouseClick += this.LoggingHandler;
```

In this case, the event handler method is declared like this:

```
private void LoggingHandler(object sender, EventArgs e)
{
    // ...
}
```

See what we just did? We used the common super-type System.EventArgs on our general-purpose logging handler. Thanks to C#'s delegate covariance and contravariance feature, this is allowed, providing more flexibility when matching method signatures against delegate types. Parameter types are treated contravariantly, while return types are treated covariantly.

# # A Sneak Peek at the Future

Now that we’ve seen the current state of affairs of the C# language, let’s talk a bit about the influences that are shaping the language’s future.

# ## Multiparadigm

Traditionally, programming languages have been classified based on the paradigms on which they’re based:

+   - Imperative programming languages use statements to modify the state of a program. Those languages are very machine-oriented and reflect how the underlying hardware works, hence giving developers low-level control over the system. Writing software following this paradigm is about stating “how” execution needs to happen, not just about “what” the problem is that needs to be solved. The earliest imperative programming language was FORTRAN, and popular descendants include COBOL, BASIC, Pascal, and C.