And then it falls off the end and completes.

Kind of monotonous, right? I mean, it just brainlessly goes to the next instruction every time.

What if you want to transfer the program flow elsewhere instead of just blindly going to the next instruction?

This is where you get your first taste of what it means to be a developer. You can ask the computer to make smart decisions based on the criteria you specify. Figuring out which criteria to specify is the job of a programmer and where most of the hard work comes in.

Eventually, we're going to code up things that say “If some condition is true, do one thing” or “If some condition is false, do another thing”.

But before that, we have to meet someone: George Boole.

# 6.4 Boolean Algebra and Expressions

Problem-solving step: Understanding the Problem.

George Boole¹ was quite an interesting character. From humble beginnings in the early 1800s, he went on to develop the mathematics that became, in many ways, the foundation of modern computation. Pretty awesome.

What he developed is what we call today Boolean Algebra.

Don’t worry—it’s easier than that algebra you’re thinking of. In fact, you already know it, just not formally and not by that name.

With Boolean, we’re interested in whether or not expressions are true or false. And then we can make decisions on whether or not they are.

Let’s do some human ones before we get into the computer stuff.

Level: Easy. Are these expressions true or false for you?

+   - I live in North America.
+   - It’s raining right now.
+   - Cats are superior to dogs.

Hopefully, that wasn’t particularly challenging. Let’s take it up a notch by introducing the concept of AND. For these, the entire expression is true only if all subexpressions are true.

For example, the statement “I’m over 190 cm tall AND I’m under 30 years of age” is false. Though I am over 190 cm tall, am I not under 30 years, so the entire expression is false.

By comparison, “I like dogs AND I like motorcycles” is true, because both of those subexpressions are true.

And if neither of them is true, the result is also false.

Level: Intermediate. Are these expressions true or false for you?

+   - I live in Europe AND I’m older than 25.
+   - It’s raining right now AND it’s sunny right now.
+   - Cats are superior to dogs AND dogs are superior to cats.

All right! Let’s do a variant on AND, namely OR. With OR, the entire expression is true if either or both of the subexpressions is true.

For example, I don’t like running, but I do like bicycling. Nevertheless, the following statement is true, because at least one of the subexpressions is true: “I like running OR I like bicycling”. True.

This is the basis for the smarty-pants answer to the question:

> Would you like soup or salad?