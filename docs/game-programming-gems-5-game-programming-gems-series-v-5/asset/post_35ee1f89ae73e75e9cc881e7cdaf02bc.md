
bet on an untested game concept from a new hire fresh out of school is challenging, admittedly:

As a result we've recently begun to see a rapid increase in the number of independently developed games, game mods, and casual games from small, young development teams. These small teams are able to test out risky ideas, and whether the results are successful or not, they're great experience for all involved—and excellent material for a resume. Those projects that are successful are an interesting opportunity for forward-thinking publishers.

The growth in demand for formal game development education is the fuel that feeds the fires of innovation in the indie game scene. Many publishers are continuing to simply evolve game concepts and play it safe, but revolutionary concepts can come from the independent game developer community, if we support it.

For professional developers, this means it's more important than ever for you to get out there and share your expertise with students and hobbyists. There are also more opportunities than ever for you to do so. Who knows, perhaps by working with a small group of independent developers on a risky game design, you'll find your own game development projects enriched and more exciting as a result.

## Preface

Kim Pallister, Intel Corporation

Kim.Pallister@Intel.com

Why am I the editor of this book?

Why am I the editor of this book? This is a book about game development, and I am not a professional game developer. I have been on the “fringes” of the industry for the past dozen years, with Intel for the past seven years, and with a graphics hardware vendor before that. In an industry that has traditionally catered to a young market, and attracted a similar vein of people to its ranks, this places me part way between bushy-tailed neophyte and grizzled curmudgeon.

Those of curmudgeon age will remember that during the first few decades of this industry, we saw a transition from one-person-shop development to an era of teams, where people relied on one another’s skills and efforts to realize their creative visions. During the past decade, and perhaps the few years that preceded it, we have transitioned to an age where groups of people rely on each other. Groups of programmers and artists and designers make up development teams. Teams within a company leverage one another’s tools and assets, and companies rely on one another at the meta level.

Inter-company relations aren’t new to the business; the developer-publisher relationship has existed for a long time. But the past decade has ushered in new structures, dependencies, and channels of communication. Developers now license technology from other companies, looking to middleware, hardware, and platform vendors for knowledge on how to exploit new technology. In return, these vendors seek information on how to direct their technology efforts. Entities like CMP Game Group (Game Developer Magazine, Game Developer Conference) and the International Game Developers Association foster dialogs about design, business practice, and quality of life issues. A growing number of academic institutions, along with publishers like Charles River Media (who brings us the Gems series), work to educate and inform the entire cluster. Looking at all these relationships, we see a circle of life—one that is inherent to all successful industries.

However slowly, the industry is moving from a state of begrudging cooperation to open, directed facilitation. We are sharing source code with middleware and hardware companies and funding research in academic circles while increasing dialog and publication. Each member of the circle has a vested interest in the success of the medium and of those who create it. That circle includes me, and *that's* why I'm editing this book.

## Where Do We Go from Here?

The near future is clear enough. The market will continue to grow as new users come on line (in both senses of the term), existing users grow older and continue to play, and the production quality of games increases, which in turn attracts users who previously weren't avid gamers.

One of the most difficult and important inflection points facing our industry is the move to multithreaded platforms and software development. At the time of this writing, desktop PCs are exposing multithreading technology in processors, and true multicore processors are around the corner. Server-side components of online games are being developed on multiprocessor and distributed systems, and the next generation of consoles promises to bring multiprocessor platforms to consumer living rooms in short order.

The transition to true multithreaded game engines and platforms looks to be a formidable challenge. We'll need new tools, new techniques, and even new languages if we hope to make this transition while still evolving our games. We'll also need to focus on sound software engineering—principles *and* practices. Projects with budgets of seven or eight (or—dare we say it—nine) figures with significantly larger teams will require a new level of discipline and rigor.

During this transition, knowledge sharing (between individuals, between companies—at all levels) will be critical. I'd like to think that the *Game Programming Gems* series will play a small part in this journey.

## Further down the Road

Looking beyond the immediate future, things get fuzzier, but exciting! At the time of this writing, Asia (particularly Korea and China) is seeing an explosion in popularity of massive multiplayer online games. Several hundred million new broadband households will appear over the next four years. Game-capable cell phones and portable devices will continue to proliferate and connect. Televisions and other consumer electronics devices will become increasingly interactive. And if it interacts, it games!

Many in our industry have been quick to draw comparisons between our games and Hollywood movies. Usually the comparisons are between the revenues that the respective industries generate or between the similarities in the production processes. Another parallel exists.

At the 1939 World's Fair, a new technology was introduced that promised to entertain people: the television. Critics were skeptical. A *New York Times* article stated “The problem with television is that people must sit and keep their eyes glued on a screen; the average American family hasn’t the time for it.” Laughable now, but no one at that time, even proponents of the technology, could have imagined the impact that this new entertainment medium would have.

During a GDC session a number of years ago, Chris Hecker forecasted that gaming would be “The defining entertainment medium of the twenty-first century,” and I can’t think of a better way to put it. We are only just beginning to grapple with the possibilities of interactive entertainment mediums. We may call that interactive entertainment “games” today, but already, we’re stretching the definitions and boundaries of the term; we are still figuring out what it all means.

Now it’s up to you to play a role in defining that medium. Hopefully we’ve given you some tools to help you do so. Put them to good use forging your contribution to the future.

## Acknowledgments

I opened this preface questioning my position as the editor of this book. Let me close by saying that I could not have done it without the direct and indirect contributions of a lot of people. At the top of my list are series editor Mark DeLoura and series publisher Jennifer Niles. I’d like to thank both for giving me the opportunity and guiding me through the journey with sage “Book Editing Gems” learned through the production of Game Programming Gems 1 through 4.

While this work represents a lot of my time and effort, it would certainly not have been possible without the many authors of the individual gems and the seven section editors:

- General Programming: William E. Damon III, ATI Research
- Mathematics: Eric Lengyel, Terathon Entertainment
- Artificial Intelligence: Robin Hunicke, Northwestern University
- Physics: Michael Dickheiser, Red Storm Entertainment
- Graphics: Jason Mitchell, ATI Research
- Network and Multiplayer: Shekhar Dhupelia, Studio Gigante
- Audio: Mark DeLoura, Sony Computer Entertainment

We really are privileged to work in an industry where knowledge-sharing is encouraged and practiced by so many.

On a similar note, Pete Baker and the rest of my management at Intel deserve thanks for letting me contribute to the greater good. When I was adamant that working on this text wouldn’t impact my day job, they knew better and let me do it anyway.

The biggest gratitude of all is owed to my wife, Alisa, for helping me pursue my passions in editing this text. Doing so during the same year that we welcomed our set of twins into the world meant a great deal more work for her as well as for me. Finally, a note of thanks is due to my mother and father, for instilling in me an insatiable curiosity about, well, everything (and for buying the Commodore64, which seems like a pretty good investment in retrospect).
