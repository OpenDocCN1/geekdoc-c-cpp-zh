sure to check for those that specifically offer HTML controls. Telerik, for example, provides calendar, chart, and gauge controls, among others.

If none of those libraries meet your needs, you'll need to write a control of your own. Do consider using the HtmlControl or even WinJS.UI.Pages if what you need is mostly a reusable block of HTML/CSS/JavaScript without custom methods, properties, and events. Along similar lines, if what you need is a reusable block of HTML in which you want to do run-time data binding, check out WinJS.Binding.Template, which we'll see in Chapter 6. The Template isn't a control as we've been describing here—it doesn't support events, for instance—but it might be exactly what you need.

When you do need to implement a custom control, everything we've learned about WinJS controls applies. WinJS, in fact, uses the exact same control model, so you can look at the WinJS source code anytime you like for a bunch of reference implementations.

But let's spell out the pattern explicitly, recalling from our earlier definition that a control is just declarative markup (creating elements in the DOM) plus applicable CSS, plus methods, properties, and events accessible from JavaScript. Here are the steps:

+   1. Define a namespace for your control(s) by using WinJS.Namespace.define to both provide a naming scope and to keep excess identifiers out of the global namespace. (Do not add controls to the WinJS namespace.) Remember that you can call WinJS.Namespace.define many times for the same namespace to add new members, so typically an app will just have a single namespace for all its custom controls no matter where they're defined.
+   2. Within that namespace, define the control constructor by using WinJS.Class.define (or derive), assigning the return value to the name you want to use in data-win-control attributes. That fully qualified name will be <namespace>.<constructor>.
+   3. Within the constructor (of the form <constructor>(element, options) ):
+      a. You can recognize any set of options you want; these are arbitrary. Simply ignore any that you don't recognize.
+      b. If element is null or undefined, create a div to use in its place.
+      c. Assuming element is the root element containing the control, be sure to set element.winControl=this and this.element=element to match the WinJS pattern.
+      d. Call WinJS.Utilities.addClass(this.element, "win-disposable") to indicate that the control implements the dispose pattern (see #5 below). Also set this._disposed = false. Alternately, use WinJS.Utilities.markDisposable (see the next section, "Implementing the Dispose Pattern"), which encapsulates these steps and parts of #5.
+   4. Within WinJS.Class.define, the second argument is an object containing your public methods and properties (those accessible through an instantiated control instance); the third argument is an object with static methods and properties (those accessible through the class