
***Programmer:*** Wait. You asked me for the most honest estimate.

***Me:*** Right.

***Programmer:*** And I said I don’t know.

***Me:*** Right.

***Programmer:*** So, what it is?

***Me:*** I don’t know.

***Programmer:*** Well, then, how do you expect me to know?

***Me:*** You already said it?

***Programmer:*** Said what?

***Me:*** I don’t know.

The most honest estimate you can give is “I don’t know.” But that estimate is not particularly accurate or precise. After all, you do know *something* about the estimate. The challenge is to quantify what you do and don’t know.

First, your estimate must be accurate. That doesn’t mean you give a firm date—you don’t dare be that precise. It just means that you name a range of dates that you feel confident in.

So, for example, sometime between now and ten years from now is a pretty accurate estimate for how long it would take you to write a hello world program. But it lacks precision.

On the other hand, yesterday at 2:15 a.m. is a very precise estimate, but it’s probably not very accurate if you haven’t started yet.

Do you see the difference? When you give an estimate, you want it to be honest both in accuracy and in precision. To be accurate, you name a range of dates within which you are confident. To be precise, you narrow that range up to the level of your confidence.

And for both of these operations, brutal honesty is the only option.

To be honest about these things, you have to have some idea of how wrong you can be. So let me tell you two stories about how wrong I once was.

## Story 1: Vectors

The year was 1978. I was working at a company named Teradyne, in Deerfield, Illinois. We built automated test equipment for the telephone company.

I was a young programmer, 26 years old. And I was working on the firmware for an embedded measurement device that bolted into racks in telephone central offices. This device was called a COLT—central office line tester.

The processor in the COLT was an Intel 8085—an early 8-bit microprocessor. We had 32K of solid-state RAM and another 32K of ROM. The ROM was based on the Intel 2708 chip, which stored 1K × 8, so we used 32 of those chips.

Those chips were plugged into sockets on our memory boards. Each board could hold 12 chips, so we used three boards.

The software was written in 8085 assembler. The source code was held in a set of source files that were compiled as a single unit. The output of the compiler was a single binary file somewhat less than 32K in length.

We took that file and cut it up into 32 chunks of 1K each. Each 1K chunk was then burned onto one of the ROM chips, which were then inserted into the sockets on the ROM boards.

As you can imagine, you had to get the right chip into the right socket on the right board. We were very careful to label them.

We sold hundreds of these devices. They were installed in telephone central offices all over the country and—indeed—the world.

What do you think happened when we changed that program? Just a one-line change?

If we added or removed a line, then all the addresses of all the subroutines after that point changed. And because those subroutines were called by other routines earlier in the code, every chip was affected. We had to reburn all 32 chips even for a one-line change!

It was a nightmare. We had to burn hundreds of sets of chips and ship them to all the field service reps all around the world. Then those reps would have to drive hundreds of miles to get to all the central offices in their district. They’d have to open our units, pull out all the memory boards, remove all 32 old chips, insert the 32 new chips, and reinsert the boards.

Now, I don’t know if you know this, but the act of removing and inserting a chip into a socket is not entirely reliable. The little pins on the chips tend to bend and break in frustratingly silent ways. Therefore, the poor field service folks had to have lots of spares of each of the 32 chips and suffer through the inevitable debugging by removing and reinserting chips until they could get a unit to work.

My boss came to me one day and told me that we had to solve this problem by making each chip independently deployable. He didn’t use those words, of course, but that was the intent. Each chip needed to be turned into an independently compilable and deployable unit. This would allow us to make changes to the program without forcing all 32 chips to be reburned. Indeed, in most cases, we could simply redeploy a single chip—the chip that was changed.

I won’t bore you with the details of the implementation. Suffice it to say that it involved vector tables, indirect calls, and the partitioning of the program into independent chunks of less than 1K each.

2. That is, each chip was turned into a polymorphic object.

My boss and I talked through the strategy, and then he asked me how long it would take me to get this done.

I told him two weeks.

But I wasn’t done in two weeks. I wasn’t done in four weeks. Nor was I done in six, eight, or ten weeks. The job took me twelve weeks to complete—it was a lot more complicated than I had anticipated.

Consequently, I was off by a factor of 6. Six!

Fortunately, my boss didn’t get mad. He saw me working on it every day. He got regular status updates from me. He understood the complexities I was dealing with.

But still. Six? How could I have been so wrong?

## Story 2: pCCU

Then there was that time, in the early 1980s, when I had to work a miracle.

You see, we had promised a new product to our customer. It was called CCU-CMU.

Copper is a precious metal. It’s rare and expensive. The phone company decided to harvest the huge network of copper wires that it had installed all over the country during the last century. The strategy was to replace those wires with a much cheaper high-bandwidth network of coaxial cable and fiber carrying digital signals. This was known as *digital switching*.

The CCU-CMU was a complete re-architecture of our measurement technology that fit within the new digital switching architecture of the phone company.

Now, we had promised the CCU-CMU to the phone company a couple of years before. We knew it was going to take us a man-year or so to build the software. But then we just never quite got around to building it.

You know how it goes. The phone company delayed their deployment, so we delayed our development. There were always lots of other, more urgent issues to deal with.

So, one day, my boss calls me into his office and says that they had forgotten about one small customer who had already installed an early digital switch. That customer was now expecting a CCU/CMU within the next month—as promised.

Now I had to create a man-year of software in less than a month.

I told my boss that this was impossible. There was no way that I could get a fully functioning CCU/CMU built in one month.

He looked at me with a sneaky grin and said that there was a way to cheat.

You see, this was a very small customer. Their installation was literally the smallest possible configuration for a digital switch. What’s more, the configuration of their equipment just happened—just happened—to eliminate virtually all of the complexity that the CCU/CMU solved.

Long story short—I got a special-purpose, one-of-a-kind unit up and running for the customer in two weeks. We called it the pCCU.

### The Lesson

Those two stories are examples of the huge range that estimates can have. On the one hand, I underestimated the vectoring of the chips by a factor of six. On the other, we found a solution to the CCU/CMU in one-twentieth the expected time.

This is where honesty comes in. Because, honestly, when things go wrong, they can go very, very wrong. And when things go right, they can sometimes go very, very right.

This makes estimating, one hell of a challenge.

### Accuracy

It should be clear by now that an estimate for a project *cannot* be a date. A single date is far too precise for a process that can be off by as much as a factor of 6, or even 20.

Estimates are not dates. Estimates are ranges. Estimates are *probability distributions*.

Probability distributions have a mean and a width—sometimes called the *standard deviation* or the *sigma*. We need to be able to express our estimates as both the mean and the sigma.

Let’s first look at the mean.

Finding the expected mean completion time for a complex task is a matter of adding up all the mean completion times for all of the subtasks. And, of course, this is recursive. The subtasks can be estimated by adding up all the times for the sub-subtasks. This creates a tree of tasks that is often called a work breakdown structure (WBS).
