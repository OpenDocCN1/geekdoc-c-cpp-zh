(virtual is the default unless a member is sealed). As such, the most derived implementation will be invoked. Wherever, IExecuteProcessActivity.InternalRun() invokes RedirectStandardOut(), the implementation on ExecuteProcessActivity() will execute instead of the implementation from IExecuteProcessActivity.

A derived type's implementation can potentially provide a method that matches a sealed signature in the parent. For example, if ExecuteProcessActivity provides a Run() that matches the signature of Run() in IWorkflowActivity, the implementation associated with the type will execute, rather than the derived implementation. In other cases, Program.Main()'s invocation of ((IExecuteProcessActivity)activity).Run() calls IExecuteProcessActivity.Run(), while activity.Run() calls ExecuteProcessActivity.Run()==where activity is of type ExecuteProcessActivity.

In summary, the encapsulation available with protected interface members, along with the other member modifiers, provides a comprehensive mechanism for encapsulation—albeit an admittedly complex one.

# Extension Methods versus Default Interface Members

When it comes to extending a published interface with additional functionality, when is it a default interface member preferable to creating an extension method or creating a second interface that derives from the first and adds additional members? The following factors should be considered when making this decision:

+   - Both conceptually support overiding by implementing a method of the same signature on an instance of the interface.

+   - Extension methods can be added from outside the assembly that contains the interface definition.

+   - While default interface properties are allowed, there is no instance storage location available (fields are not allowed) for the property value, limiting the applicability to calculated properties.