into the sequence, the 32-digit hex number could be seen as a handy shorthand for
its source sequence.

On the face of it, this might seem like a neat way of generating a unique identifieror the amino acid sequences we've been asked to manage in this scenario. But there
are a number of pitfalls.

The first is that a number of flaws in the MD5 algorithm means that there is nowhere
ear as 'collision resistance' as first thought, and that it's actually quite straight-
forward artificially construct two input sequences that 'collide' to give the same
output. For security applications, this is disastrous, but means that MD5 is a risk that's not
worth asking. Other, more recent hashing algorithms (such as SHA-256) are much
more resistant to collisions, and therefore more suitable replacements for MD5.

Whereas the first pitfall is one of balancing probabilities – the risk of an accidental
collision or the consequences of malicious manipulation – the second concern is much
more fundamental, and hinges on the idea that hashing to generate an identity
breaks the principle of opacity discussed in Section 7.3. Although 2277d9c488b-
82cf17dc1908fb338a appears opaque to humans, and in that there is no way of figuring
out what sequence it refers to just by inspecting the hexadecimal signature, using this
mechanism creates a strong semantic link between the sequence and the identifier (as
t latter was generated from the former). This is always a bad thing to do. If we
example, consider a situation where an error is found in the amino acid sequence,
t that it is computationally possible to see that an update to the original
sequence has happened (rather than by just fixing the sequence in it), even with
a semantically untied situation, as the hashed signature is now inconsistent with
the sequence of bytes that generated it in the first place. Does this really matter if we treat it as being semantically opaque, but in that case, worthy with the hashing at all? As it might sound, an integer
cremented for each record, and quite suited with a namespace would have done
t job far better and with fewer chances of confusion.

+   2 The slight strangeness that remains in the format of http-URI URLs comesrom the inclusion of the domain name component. Domain names, such as
www.uniqprot.org, when left to right, start off with quite specific and get more
gen (the machine called 'www', in a domain called 'uniqprot', which is a kind of
'organisation'). URLs, on the other hand, get specific when read left to right
(this is a kind of http URI, hosted by this particular domain, referring to this set of
resources, and specifically to this particular called P02699. Although this may
rankle with computer-science purists, in practice, this oddity doesn't cause any real
problems.

# Chapter 8

+   1 It's really hard to tell how many times 'Defrosting the Digital Library' has been cited
– and any numbers that you've found should probably be taken with a large pinch
of salt. In February 2015, for example, Google Scholar suggested 159 citations,
whereas Scopus gave 59; it's very hard to tell which of these is the more accurate,