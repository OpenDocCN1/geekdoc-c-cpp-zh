
If readers can understand your intention, they will have greater confidence when changing the code and tests as intentions for the software change.

To this end, ***simpler architecture, design and code should focus on maximising human comprehension by effectively documenting intent and minimising cognitive overhead*** in the person struggling to comprehend your software.

Prefer clarity of intent in your code and avoid anything that introduces confusion, such as surprise!

## Axiom 4: Mechanical Sympathy is Queen

> "to get the best out of any car, you have to have a sympathy for how it actually works and then you can work in harmony with it," Jackie Stewart

Mechanical Sympathy may have its roots in Formula 1 car racing, that high speed processional sport that we Brits love, but Martin Thompson has importantly re-introduced this facet of thinking into the code we design and write.

Mechanical Sympathy is a philosophical approach to designing and writing software whereby *the consumer of your software, in this case the machine, is primarily considered*. The nuances of the underlying machine are clearly understood and have a large effect on the code you write as you strive to make the most of what the machine is trying to accomplish. This approach is particularly important *where low latency is crucial to the success of a piece of software*.

*Mechanical sympathy and maximising for human comprehension can seem to be at odds with one another. However to place the two as distinct competing forces can result in a false dichotomy.*

*As long as human comprehension has been thought about and optimised for then applying the tenets of machine sympathy to compromise some aspect of comprehension where applicable is a useful and appropriate secondary goal.*

## Axiom 5: Software is a process of *Research & Development*

> *“We don’t know what we’re doing...”, “You are not a software developer, you make change happen and software is just one tool...”*

We don’t know what we’re doing and that’s ok! Perhaps it might be more accurate to state that we don’t know *exactly* what we’re aiming for when developing software, especially when embracing the natural change that occurs.

When embarking on building a software solution, arguably even before we decide that any software is needed at all, we embark on a *journey of research and discovery*. Our research will span everything from the concepts and language used in the problem space we’re addressing right through to the best tools, techniques and languages we can employ to produce the change needed to address those problems.

*We are researchers and developers* and this has wide-ranging impacts on how we manage our work. Recognising the importance of research and discovery in software solution development shifts our thinking from the factory floor (i.e. let’s just churn out some more widgets!) to the status of change agents and problem solvers. Software is often our answer, but we are also responsible for exploring, understanding and researching the problem space because, more frequently than not, this is poorly understood even by those who believe they know what is needed.

## Axiom 6: Software Development is an extremely challenging Intellectual Pursuit

This might come as a surprise to some but *software development really doesn't happen when someone is hammering enthusiastically, or not, on a keyboard*. That, as those of us in the trade would say, is just the 'output'. *The hard part has already been done.*

Software is *designed in the mind, collaboratively in conversation and on whiteboards* before it goes anywhere near turning it into characters of text in a program. *The majority of the effort in software development is in understanding what might be needed, and then turning that into a design that can deal with the test of time.*

It is that test of time, the ultimate stressor on a design, that this book aims to help with.

*When developers are thinking, they are working.* When they are typing, they are turning their hard work into something that can be used. Unfortunately thinking is very hard and, when it comes to software and the variability of understanding what people might want, this *places software development firmly in the camp of the most vital and intellectually challenging jobs of the 21st century.*

## What are we really dealing with, then?

This book is not anti- or pro anything other than helping you succeed in designing and deploying better software and doing more with your life. I believe, and have personally first- and second-hand witnessed, benefits from using the techniques discussed in this book where groups of people are tasked with the confusing and ephemeral task of ‘building software’.

Too much time is wasted building the wrong thing, or building something that takes herculean levels of effort to keep it stumbling forward like a drunk sumo wrestler up a hill. The key challenges of software development can be distilled into two areas:

- *How do I avoid Over Production?* We're creating too much software, and what we do create is often not valuable.
- ***How do I create and maintain software that adapts as fast as the needs placed upon it?*** We need to create software that meets the needs of ubiquitous and accelerating change.

For the more Twitter-friendly audiences, these two challenges can be simplified to:

- Challenge 1: Building the right thing (or not building anything at all!)
- *Challenge 2: Building the right thing, right*

This book focusses on Challenge 2 and can be thought of as a set of weapons for defeating that particular bully.

![](img/6aa0b2c29d7992041f99024e15f60a20_29_0.png)

Camilla's Bookshop, Eastbourne. My favourite bookshop in the world, featuring the amazing owner Camilla in this photo. A bookshop that is as exciting as the books it holds. Never boring.

## A Nod Towards Over-Production

Before we move on to the main challenge of this book, there’s a little context-setting I’d like to do on the subject of “Building the right thing” as it relates to where the various destinations that the rest of this book intends to take you on a journey to.

Over Production is a Lean Waste, and it is on the increase in Software Development across the industry. For our purposes, Over Production can be defined as building the wrong thing.

This includes the cases of building the right thing at the wrong time, and of course the wrong thing at the right time. The temporal characteristic of rendering a product the wrong thing is included in the general definition of building the wrong thing.

As software developers learn to organise and complete their work more efficiently using work management techniques such as Agile processes, the potential for greater productivity is unlocked. At least greater productivity potential is unlocked while the challenges of reacting quickly to change through adaption can be kept under control.

The flip side of this productivity is that it is much more likely to produce the wrong thing. Increased efficiency does not lead to increased effectiveness of what is produced.

![](img/6aa0b2c29d7992041f99024e15f60a20_31_0.png)

You wish your software development engine was even half this sexy, or effective.

If viewed as an engine of software production, it could be argued that current Agile and Craftsmanship techniques in the software development industry are having huge impacts in helping that engine fire on all cylinders. However taking the analogy a step further, the engine may be firing on all cylinders but the direction the engine is heading in, and its ability to change course, is an entirely different matter.

Even if you apply the patterns and techniques from this book to help you build the right thing, right, i.e. build adaptable software, that is only an important *enabler* that supports the possibility of building the right thing. It does not guarantee that useful software will be an outcome. For more on techniques that work towards overcoming that problem, take a look in the **Further Reading** chapter at the end of this book.

That said, *architecting and building software that enables you to build the right thing continuously is no mean feat*, so we begin our journey with the ***biggest barrier to a piece of software being adaptable...***
