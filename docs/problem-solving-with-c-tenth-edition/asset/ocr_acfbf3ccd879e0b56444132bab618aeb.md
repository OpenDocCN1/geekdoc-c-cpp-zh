![](bbox=[0.07, 0.08, 0.2, 0.22])

After a lecture on cosmology and the structure of the solar system, William James was accosted by a little old lady.
"Your theory that the sun is the center of the solar system, and the earth is a ball which rotates around it has a very convincing ring to it, Mr. James, but it's wrong. I've got a better theory," said the little old lady.
"And what is that, madam?" inquired James politely.
"That we live on a crust of earth which is on the back of a giant turtle."
Not wishing to demolish this absurd little theory by bringing to bear the masses of scientific evidence he had at his command, James decided to gently dissuade his opponent by making her see some of the inadequacies of her position.
"If your theory is correct, madam," he asked, "what does this turtle stand on?"
"You're a very clever man, Mr. James, and that's a very good question," replied the little old lady, "but I have an answer to it. And it is this: the first turtle stands on the back of a second, far larger, turtle, who stands directly under him."
"But what does this second turtle stand on?" persisted James patiently.
To this the little old lady crowed triumphantly. "It's no use, Mr. James—it's turtles all the way down."

J. R. ROSS, Constraints on Variables in Syntax

# INTRODUCTION

You have encountered a few cases of circular definitions that worked out satisfactorily. The most prominent examples are the definitions of certain C++ statements. For example, the definition of a while statement says that it can contain other (smaller) statements. Since one of the possibilities for these smaller statements is another while statement, there is a kind of circularity in that definition. The definition of the while statement, if written out in complete detail, will contain a reference to while statements. In mathematics, this kind of circular definition is called a recursive definition. In C++, a function may be defined in terms of itself in the same way. To put it more precisely, a function definition may contain a call to itself. In such cases, the function is said to be recursive. This chapter discusses recursion in C++ and more generally discusses recursion as a programming and problem-solving technique.

# PREREQUISITES

Sections 14.1 and 14.2 use material only from Chapters 2 through 5. Section 14.3 uses material from Chapters 2 through 7 and 10.