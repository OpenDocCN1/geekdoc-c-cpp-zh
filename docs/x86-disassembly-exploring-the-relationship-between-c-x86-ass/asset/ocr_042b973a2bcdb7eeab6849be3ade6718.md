# # 13 Branches

# ## 13.1 Branching

Computer science professors tell their students to avoid jumps and **goto** instructions, to avoid the proverbial 'spaghetti code.' Unfortunately, assembly only has jump instructions to control program flow. This chapter will explore the subject that many people avoid the plague, and will attempt to show how the spaghetti of assembly can be translated into the more familiar control structures of high-level language. Specifically, this chapter will focus on **If-Then-Else** and **Switch** branching instructions.

# ## 13.2 If-Then

Let's consider a generic **if** statement in pseudo-code followed by its equivalent form using jumps: