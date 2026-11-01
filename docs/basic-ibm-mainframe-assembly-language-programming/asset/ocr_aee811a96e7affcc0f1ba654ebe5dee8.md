# 1. Preface

# 1.1 Goals

The goals of this book are to give the reader a basic understanding of the IBM mainframe architecture from the perspective of the instruction set and to serve as an assembly language text for introductory college courses in computer organization. The text originally began as a set of class notes for an undergraduate computer science course on Computer Organization. Over the years it has been expanded and enlarged to the text you see here.

Many computer architectures have come and gone in the past 50 years and only a relatively few designs remain in production today. In the early 90s, the rapid rise of new computer manufacturers such as Sun, Apollo, Silicon Graphics, MIPS, Digital Equipment Corporation (DEC), Tandem, Prime, Data General, SDS (also known as XDS) and many more seemed to point to a world without the mainframes. All these, however, are now gone along with several legacy mainframe manufacturers such as NCR, Burroughs, Control Data Corporation, General Electric, Honeywell, RCA and UNIVAC (UNIVAC and Burroughs merged to form UNISYS which still manufactures a limited line of mainframes).

In the not too distant past it was assumed that the rise of microprocessors and server centric computing would bring an end to the age of big iron as mainframes were referred to.

But the IBM mainframe architecture has endured and, rather than declining, is growing in popularity and becoming the platform of choice for such rapidly emerging technologies as cloud computing and virtualization. As the world chokes in an energy and space intensive microprocessor based server sprawl, a single mainframe system can deliver thousands of virtual Linux platforms for a fraction of the cost in dollars, energy and space.

While most computer users are familiar with the ubiquitous Intel x86 microprocessor line, few have had any experience with another widely used architecture, the IBM mainframe.

As the baby-boom generation programmers who wrote the billions of lines of mainframe assembly language code since the introduction of the IBM 360 in 1964 are beginning to retire, the demand for replacement programmers to maintain, support and extend these applications as well as develop new ones is growing rapidly. To those looking to meet this need, this text will serve as a basic road map and introduction to the fundamentals of the architecture.