![](bbox=[0.125, 0.094, 0.878, 0.568])

FIGURE 8.4: Checking conformance in the enterprise viewpoint.

We now have our observations in terms of a sequence of computational signals. The next step is to interpret these as operations performed by particular processes. This is a nontrivial task, since it is necessary to pair-up requests and responses and disentangle concurrent threads of execution, and it may involve building up the necessary context by finding suitable correlators, like session or transaction identifiers. Finally, these computational interactions must be interpreted using the next set of correspondences to identify the enterprise interactions and the roles that are responsible for them.

As we move up to progressively more abstract representations, we need to draw upon knowledge of the context involved that has been acquired by analysis of earlier observations. In some cases, the initial analysis may be ambiguous, with further observation being necessary to determine, for example, which of the roles an object holds is responsible for its rejecting a request.

Of course, anywhere in this chain, the analysis may fail. Such failures indicate a failure to obey the rules of the view concerned, and so indicate a