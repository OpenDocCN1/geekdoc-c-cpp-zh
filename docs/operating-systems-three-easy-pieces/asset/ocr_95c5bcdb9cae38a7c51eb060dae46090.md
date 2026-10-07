# A Dialogue on Concurrency

**Professor:** And thus we reach the second of our three pillars of operating systems: concurrency.

**Student:** Umm... I thought there were four peaches...?

**Professor:** Nope, that was in an older version of the book.

**Student:** (interrupting) Peaches again! What is so with concurrency, oh wonderful professor?

**Professor:** Well, imagine we have a peach —

**Student:** (interrupting) What is it with you and what peaches?

**Professor:** Ever read T.S. Eliot? The Love Song of J. Alfred Prufrock, “Do I dare to eat a peach”, and all that fun stuff?

**Student:** Oh yes! In English class in high school. Great stuff! I really liked the part

**Professor:** (interrupting) This has nothing to do with that — I like peaches. Anyway, imagine there are a lot of peaches on a table, and a lot of people who want to eat them. Let's say we did this way: each eater first identifies a peach visually, and then tries to grab it and eat it. What is wrong with this approach?

**Student:** Hmmm... seems like you miss a peach that somebody else also sees. If they get there first, when you reach out, no peach for you!

**Professor:** Exactly! So what should we do about it?

**Student:** Well, probably develop a better way of going about this. Maybe form a line, and when you get to the front, grab a peach and get on with it.

**Professor:** Good! But what's wrong with your approach?

**Professor:** Yes.

**Student:** OK, let me think. Well, we used to have many people grabbing peaches all at once, which is faster. But in my way, we just go one at a time, which is correct, but quite a bit slower. The best kind of approach would be fast and correct, probably.