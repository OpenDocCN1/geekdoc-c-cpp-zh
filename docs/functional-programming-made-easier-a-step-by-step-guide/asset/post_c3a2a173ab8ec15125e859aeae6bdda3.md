
-  30.9. Calling the Backend ........................................................ 1705
-  30.9.1. CORS Solution ............................................................. 1724
-  30.9.2. Static File Server Solution .............................................. 1727
-  30.10. ChangePassword Page ....................................................... 1740
-  30.11. Users Page ................................................................. 1748
-  30.12. Modal Dialog Component ..................................................... 1791
-  30.13. Message Modal Component .................................................... 1799
-  30.14. Customizing the Modal Dialog Component .................................... 1810
-  30.15. Create Users Modal Component .............................................. 1825
-  30.16. Logoff Page ............................................................... 1888
-  Appendix A: Epilogue .............................................................. 1904

-  Reusable code.
-  Confidence in code correctness.
-  Elimination of unnecessary complexity.
-  Coding mostly the Happy Path.

I cannot imagine many programmers who don’t value the things on this list. We all want powerful tools that help us solve problems without requiring us to do the same work over and over again while producing code that’s predictable and maintainable.

We don’t want to deploy our code into production only for it to break requiring us to stay up all night trying to understand code that we wrote a few months ago under the pressure of production being down.

Essentially, we want to be in control of our code to minimize pain, and anything that makes our job easier and less painful is valuable to us.

If you value these things, then Functional Programming is the best and most powerful tool that we have to date to achieve everything on this list and more. That’s not to say that something more powerful may not come along in 10 to 20 years, because it could.

But unlike Imperative Programming, Functional Programming has its roots in Mathematics that goes back over 100 years and that Math is built on a foundation of Mathematics that goes back hundreds if not thousands of years. In contrast, conventional programming languages only go back about 60 years.

It is said that Mathematics is discovered not invented. This implies that Functional Programming is also discovered, whereas most other languages are simply invented. [3]

And since Mathematics has proven itself so valuable for solving complex problems in nearly every human endeavor, it’s pretty likely that Functional Programming is our best hope to control the scourge of complexity that’s pervasive in our modern software.

## You Cannot Describe an Experience

Ever hear someone say, "You had to be there"? Well, trying to explain why Functional Programming is so great is somewhat like that.

I know now that, when given the choice, I’ll never choose an Imperative Language over a Functional one ever again.

However, if you pressed me for an explanation, I’d say because the *experience* of programming in a Functional Language is just so far superior that I enjoy programming infinitely more.

Unfortunately, this explanation is terrible because I cannot describe an experience well enough so that you will understand, unless, of course, you’ve shared that experience.

It’s like trying to explain to a couple who are about to have their first baby what it’s like to become parents and how the center of their universe will now be on the child. I don’t even try explaining this. Instead, I

## Case Study: Javascript

It’s no different for software. We developers consider mostly language popularity and job prospects when choosing which language to hang our hat on. However, we rarely consider the Costs of Ownership.

One of the things I really liked about Javascript when I first started using it was how quickly I could write something and get it to work. I was coming from Java and welcomed the freedom from what I considered, at the time, "its tyrannical adherence to Types".

In the early days of Javascript, I’d sometimes get a Runtime Exception when I ran my code but I could easily and quickly fix it. Little did I realize, that this experience would scale up exponentially with the size of my program.

Having a dynamic language felt freeing and more efficient because I didn’t have to wait for it to compile and I could do "anything" to my program and "not have to worry about Types". I could have an Array that contained BOTH Strings and Numbers if I wanted to. In my mind, this was a big win regarding the development phase.

The Cost associated with writing Javascript code was far less than it was with a Statically Typed language, which is why I initially loved it.

But because Javascript isn’t compiled, it routinely crashes in the hands of users. So to combat this, the industry embraced Test Driven Development. It was all the rage and was touted to ferret out bugs and reduce Runtime Errors. Unfortunately, this approach has saddled us with the cost of having to write and maintain test code, which quickly grows to be an appreciable percentage of our codebase with its own set of bugs.

For me, this cost began to outweigh any gains I originally got from using a Dynamic Language.

## Case Study: Elm

When our company decided to use Elm instead of Javascript for our next big project, I had to train the developers in basic Functional Concepts which was a one-time, up front cost.

In the beginning, a lot of time was spent trying to decipher the compiler errors. For example, Elm has Type Inference meaning that you don’t always have to specify the Types since the compiler can infer them from how you use your variables. However, this means that the error isn’t always reported where you made your mistake.

It takes developers time to realize that they used a variable differently in two places, e.g. as a String and a Number, and that the second usage is where the error will show up. Sometimes that isn’t always the wrong usage. Maybe it’s supposed to be a Number and the usage as a String is where the real error is.

Even after this initial developer acclimation period is over, an appreciable amount of time is spent dealing with compiler error messages, i.e. mistakes made by the developer that the compiler catches. These bugs are not caught by testing code or by users, but, instead, by the compiler, code that we do not have to write specifically for our program and code that we do not have to maintain.

When we put our Elm code into production, it just seemed to work with no Runtime Errors. [5]

The Upfront Cost of Elm was huge compared to Javascript, but the Costs of Ownership were drastically reduced so much so that we are able to add complex features to our product faster than ever before.

It’s worth noting that this gain wasn’t solely because of the difference between a Statically Typed language and a Dynamically Typed one. Many of the gains in development came from the developer’s ability to more easily reason about their code and to be able to leverage powerful abstractions.

## Finding Developers

If you are involved in the hiring process and you’re reading this wondering how you’ll find trained Functional Programmers if you adopt a Functional Language at work, the answer, at the time of this writing, is that you’re probably not, at least not in your area.

If your company is open to remote workers then finding developers is not a problem. There are plenty of Developers who would gladly leave their current employment to get a chance to work in a Functional Programming Language. I saw this personally when we were hiring Elm programmers.

Also, in my experience, Functional Programmers are a cut above most. They’ve typically had to endure the hardship of learning this craft on their own time and are usually lifelong learners. Hopefully, this book will go a long way to reduce that hardship, but it will never be eliminated completely. Anything worth doing is going to require hard work.

But the truth of the matter is that you’ll most likely have to train them. I hope that this book will help you in that process and hopefully more books will be written with similar goals.

## Finding Jobs

One thing I’ve always prided myself on the fact that I always stay up to date with technology. Since, I can’t know all technologies, I have to pick and choose. The way I did this early in my career was to look at the industry and try to predict what skills would be in demand in the next 5 years.

So, will Functional Programming be a requirement in 5 years? If you asked me at the time of this writing, I’d have to say that it probably won’t be. Even though many programming languages have adopted Functional features, e.g. Java now has Lambdas, it’s still difficult to find jobs where you can program in a Functional Language.

Stories of the benefits of using Functional Programming Languages in Greenfield Projects, i.e. projects that are written from scratch, will need time to be told and retold before the industry will start to consider this approach. Also, more books to help developers get up to speed quickly will need to be written.

That’s why I believe that somewhere between 2020 and 2030, Functional Programming will become the paradigm of choice for most Greenfield Projects.

Even then, there will still be a huge need for Imperative Programmers. There’s still a need for Cobol
