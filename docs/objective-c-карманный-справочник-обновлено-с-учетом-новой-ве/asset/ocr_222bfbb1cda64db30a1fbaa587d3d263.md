associated with it.

Unlike the exception object, the dictionary has include the localized error description. You can present this to the user without any extra processing.
Error objects also sometimes include a recovery strategy. The recovery attempter object can try to automatically recover from an error. For some errors this is not possible, but often you get an error when you try to do something that is possible, but unsafe. When this happens, you should present the error to the user and then call the recovery attempter.

If you have used Common Lisp, this pattern will seem familiar as an ad-hoc form of restartable exception.