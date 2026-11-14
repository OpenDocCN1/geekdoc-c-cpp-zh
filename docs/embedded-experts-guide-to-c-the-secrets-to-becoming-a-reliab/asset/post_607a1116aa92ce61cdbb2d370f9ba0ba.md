
that many existing embedded compilers will remain largely unchanged for some time.

Second, there is no mention of Rust. The programming language – not the red stuff you find on nails. This is a book on C, so arguably there is no reason to mention any other language at all. Many are mentioned in passing, but not in detail. Why then, should Rust be any different?

Rust does deserve a special mention. Its proponents say it is the language that will finally replace C (and C++). Such claims are premature, but should not be dismissed entirely. Rust does have some benefits over C. Throughout this book, I have highlighted the many issues the C language has, most of which can be avoided by using Rust. But the same could be said of Ada, and if programming languages became popular based solely on technical merit, we would see much less C and much more Ada. Rust, however, has something more than technical merit. Since 2021, it has had the Rust Foundation, the founding members of which are Microsoft, Amazon Web Services, Huawei, Google and Mozilla. Their support, rather than the language's reputation for safety, are what I suspect is driving its seemingly unstoppable growth. By the time people started to show serious interest in Rust, this book was nearly complete. So, like C23, Rust's absence is nothing more than a case of bad timing.

There will be a market for C programmers for years to come, but at least consider learning some Rust.

In case you're wondering, the reason this book took so long to write is because C is so full of quirks and nuance. Researching it is to go down a rabbit hole. There is a great deal left unsaid in this book. I could keep working for another five years and there would still be a great deal left unsaid. Perhaps there will be a second edition, but perhaps not. I am certainly not making any promises!

## Some thanks are in order:

It is fitting that Chris Hills agreed to write the foreword to this book. Chris attended my first training course as a guest; his contribution on the day was remarkable, his feedback and advice has been invaluable. On many occasions he has been responsible for highlighting some of the issues the C Language has – these are easily missed or forgotten about, so I will share with you the same advice Chris shared with me when we first met: use a static analyser.

My publisher, Ladey Adey, and her team have made this book possible. While the words are mine, there is much more to a book - layout, typesetting and aesthetics must all be considered. There are also many publishing-specific considerations to publishing of which I was blissfully unaware – and probably still would be without the help I have received in navigating them. The team have also been remarkably patient with me! I naively suggested this book would be drafted within a year. It was not.

Eleanor, my wife, has been patient too. She has tolerated me writing a book when I probably should have been making a greater effort to earn some more immediate income.

## About the Author

![](img/605f0fb04c15ae9612ab9a8fee5ca8e7_272_0.png)

Many years before gaining a PhD, presenting a first training course or writing this book, Dr Chris Rose – who has worked as a researcher in academia and a consultant to both SMEs and global companies – learned to program by experimenting with a BASIC interpreter and later by writing assembly programs for PIC microcontrollers.

This was the beginning of a journey which led Chris to specialise in writing digital control software for power electronic converters – this has included working with electric motor controllers, electric vehicle chargers and grid-tie inverters for renewable generation.

Chris can be found on LinkedIn:
https://www.linkedin.com/in/chrisrose-ei/

## Your Notes

Here are some additional pages for your own notes.

![](img/605f0fb04c15ae9612ab9a8fee5ca8e7_275_0.png)

Countless pieces of software are written in C. Every year, thousands of students learn the language. 50 years after first being created, it remains popular – especially for embedded applications.

That popularity means a great many books have been written on how to write C. So you might – quite reasonably – ask if the world really needs another one. The answer: “probably not.”

But this is NOT another book on how to write C – it is a book on how not to write C. That is something the world desperately does need, because despite its enduring popularity, many programmers remain blissfully unaware of the issues C has or how to avoid them.

This book assumes you can already write C the way all those other books tell you to do it. Its purpose is not to repeat what you already know, but to reveal some of the nuances, curiosities and outright absurdities of the language that are all too often ignored.

![](img/605f0fb04c15ae9612ab9a8fee5ca8e7_275_1.png)
