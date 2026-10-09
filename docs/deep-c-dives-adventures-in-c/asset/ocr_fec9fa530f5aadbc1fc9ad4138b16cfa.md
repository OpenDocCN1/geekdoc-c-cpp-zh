# ## Undefined Behavior

The current concern is undefined behavior, UB – what it is, what it means and how to avoid it. However, as we have just seen, before undefined behavior hit the C headlines, we had unobservable behavior to cope with. In many ways the two are very similar, but undefined behavior takes on a more aggressive role.

Undefined behavior is a term used to specify that a particular operation has no meaning or is unpredictable. The idea is that the language specification refuses to specify what is to happen, leaving it up to someone else to supply an interpretation. This seems innocent enough, but over time it has morphed into something of a monster.

There is a great deal of argument about when the notion of undefined behavior first arose and much of it is about the placement and interpretation of commas in standards. Standards are not always particularly clear. What is clear is that, initially at least, undefined behavior was used to simply mean that the standard did not cover the situation. In this sense, if you wrote code that included undefined behavior then your program was not covered by the standard.

Perhaps the high point of undefined behavior's travel from reasonable to unreasonable was the famous “nasal demons” post in 1992 on a fairly “serious” newsgroup, comp.std.c:

> “*Undefined behavior -- behavior, upon use of a nonportable or erroneous program construct, ... for which the standard imposes no requirements. Permissible undefined behavior ranges from ignoring the situation completely with unpredictable results, to having demons fly out of your nose.*”

If you think that this humorous comment is extreme, a few posts earlier we have:

> “*At this point, the compiler is at liberty to generate a program which formats your hard disk drive. In fact, it probably should.*”

The idea that if a program contained undefined behavior then all bets were off grew and continues to grow from this point. It is the programmer's equivalent of the principle of explosion. If you have two logical premises, P and !P, and you assume that they are both true, then anything can be proved true. The reasoning is:

P is true so P or Q is true no matter what Q is. But as !P is true P or Q implies that Q is true. Hence any statement can be proved true if P and !P are assumed.

So rejecting the law that only one of P or !P can be true, leads to a situation in which logical demons can fly out of your nose.