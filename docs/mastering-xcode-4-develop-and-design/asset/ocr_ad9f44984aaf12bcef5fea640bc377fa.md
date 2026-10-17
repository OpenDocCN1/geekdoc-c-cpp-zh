# MOVING THE EXECUTION POINTER

You can drag the execution pointer and place it anywhere within the local scope.
You can use this to skip parts of code or to jump backward to repeat instructions.
To move the execution pointer, grab the green arrow along the left edge of the Source Editor and drag it to the desired instruction.

Moving the execution pointer backward to repeat instructions will not undo the instructions that were just executed. It will execute them again when you continue or step through your code. If you are new to debugging, missing this distinction can be confusing.

# USING THE DEBUG NAVIGATOR

As you learned in Chapter 3, the Debug navigator shows the threads and stacks when execution is paused in the debugger. This view represents the same information found in the Threads and Stacks navigator in the Debugger Bar. You can organize the navigator by thread or by Grand Central Dispatch queue.

You can further refine the navigator using the controls at the bottom. The button at the left side of the slider (∑), when enabled, filters the threads and stacks to show only the threads that have your code in them or for which debugging symbols exist. The slider controls how much stack detail to show—the left side shows only the top frame of each stack while the right shows all stack frames.

> **NOTE:** For more information about Grand Central Dispatch, refer to the Apple developer documentation.

# WRAPPING UP

You should now have a firm grasp of the basic debugging facilities that Xcode 4 offers. You’ll find more debugging techniques in Chapter 17. In the next chapter, you’ll explore Xcode’s graphical data modeler and use it to add some data management and storage capabilities to TestApp.

![](bbox=[0.745, 0.6, 1.0, 0.752])