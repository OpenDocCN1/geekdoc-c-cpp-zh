First of all, using namespace Municipal injects int signal_result (Result::DecisiveVictory) into the LCA of Municipal and Business. Remember that this hides previous meanings of signal_result. Can you identify what this has hidden?

It has hidden gdg::signal_result and World::signal_result. Keep that in mind.

The next using-directive introduces gdg::signal_result into the global namespace. This is the LCA of namespace gdg and namespace Business. However, that itself has been hidden by World::signal_result, which has itself been hidden by Municipal::signal_result. So which signal_result is invoked at the end of the test function?

Municipal::signal_result is the only available choice. Even though it takes a DecisiveVictory rather than a CrushingVictory, it is the best fit, being the only fit.

Did you follow that, answer the questions correctly and deduce the correct function?

Now, I appreciate that this might seem contrived and overly complicated. How-ever, this is not too dissimilar from a real-world example that utterly defeated me for the best part of a week. I have taken out all the extraneous furniture that was nothing to do with the bug to aid exposition. Imagine this code spread over a few thousand lines through a handful of source files. Imagine this code manifesting by silently recording the wrong kind of victory that was not too far from the right kind of victory. Imagine thinking that this bug is unrelated to the quality of the victory, but to the way that the details of the victory are passed to the rest of the system. Why on earth would you think that CrushingVictory would not be recorded? There it is, right there in the code. The solution only came to me when I was stepping through the code and suddenly realized that I had gone to the wrong place. I blamed the debugger and spent far too long arguing about optimizers with anyone who would listen. Perhaps a COMDAT had been incorrectly folded. But no, the error was that I didn’t understand how using-directives worked.

# An altogether more insidious problem