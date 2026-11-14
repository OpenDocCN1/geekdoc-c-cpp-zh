
the rationale behind each solution including the design tradeoffs and their consequences. Dearden and Finlay [2006] note that patterns 'capture insights about the design that can inform even an experienced designer; explaining not only how a problem can be solved but also why a design choice is appropriate to a particular context.'

Patterns naturally become a conversational language because each pattern contains a unique name that is easy to remember and use [Mezzaros and Doble, 1998]. The pattern names become a lexicon, and the specificity of the pattern descriptions lends precision to this lexicon. Pattern languages therefore are design languages facilitating communication amongst designers [Dearden and Finlay, 2006] and teams [Borchers, 2000].

Most importantly, each pattern includes several examples from real world designs. As Kohls and Uetcht [2009] point out, 'There is one section in most documented patterns that we consider as indispensable: the examples section. ... Only experience with multiple examples helps identify relevant variables.'

The structure of patterns generalizes good designs while retaining an element of concreteness [Bayle et al., 1998]. This dual nature prevents patterns from being prescriptive. Instead, they describe design spaces more than specific designs [Buschmann et al., 2007]. Because patterns are not overly specific, they enable variety in implementation. For example, Alexander's 'Entrance transition' pattern suggests using architectural features to give multiple cues of a transition from public to private place. The pattern does not prescribe a specific ground plan, but lists several patterns as options: Garden wall, Tapestry of light and dark, Trellised walk, etc. The designer can choose any of these, as well as choose how they want to realise each option that they choose. The actual design created from patterns is always an adaptation of design principles to a specific situation.

## 1.3 An illustrative example

At first glance, pattern languages can seem quite abstract. In practice, pattern languages are most easily understood through example. This section will use a pattern language for newspapers [McKaughan, 2011] to illustrate the possibilities pattern languages have for typographic or typeface design. We start by painting an overall picture of the pattern language by naming several of the patterns and describing how they work in concert.

Next, we go into more detail by listing the complete specification of one of those patterns. This is followed by a discussion which walks through that pattern in detail, highlighting the pattern structure and practical benefits.

### 1.3.1 A pattern language for news

Consider the front page of a newspaper. The brand is instantly recognizable from the overall layout and typeface choices, even before we recognize the publication logo. The weights and styles help readers navigate the page to find an article, and the text of that article is set so that it is easy to read, while packing in as much text as possible to save printing costs. The page demonstrates a number of problems and choices: some are conventions for newspapers, some reveal the brand, and some serve material necessities of the print medium. These problems and choices operate at many different levels, from overall layout to the length of serifs, and all interact to form a unified whole.

This pattern language attacks these problems by first identifying broad issues such as branding, then proceeds through increasingly more detailed patterns all the way down to the level of letterform design.

Returning to the newspaper front page: A pattern called news typographic design outlines the overall typographic requirements of newspapers – issues of brand, editorial feel, printing economy, etc. – and points towards general purpose patterns to maintain typographic identity, using a variegated typeface family composed of many styles, with an optional complementary sans-serif. The newspaper would have to employ a reading typeface and an economic text setting to give readers a comfortable reading experience while remaining within cost constraints.

News typographic design also takes advantage of genre-specific patterns such as newspaper text proportions and headline typefaces, which outline the requirements for the design of a newspaper typeface. These patterns lead to more detailed patterns for designing a typeface in this context with dark-printing letterforms with malleable joins, economic widths, and large apparent size. Media-specific patterns that describe typefaces for low-resolution screens or sturdiness for stereotyping help adapt a design to a particular medium.

The above patterns work together to set the design requirements for a newspaper. A few additional patterns can give the designer flexibility for related publications. For example, to design the Sunday magazine supplement for a newspaper, a designer might replace **economic text setting** and **newspaper text proportions** with a **luxurious text setting** and **book text proportions**, while still employing the rest of the newspaper's patterns. The result would be a much more open, magazine-like layout appropriate for a lazy Sunday morning read, while still adhering to the overall design of the publication. The magazine supplement would therefore function alongside the newspaper as a complementary member of the publication's family.

### 1.3.2 Example pattern: newspaper text proportions

The following is the complete specification for the pattern, **newspaper text proportions**, mentioned in the previous section. It illustrates typographic patterns in more detail, particularly in the way that patterns specify relationships and employ other patterns to establish problem contexts and to solve them. A discussion of this pattern's construction follows the pattern.

#### 1.3.2.1 Problem context

Morison eloquently described the context of newspaper typefaces:

> The problem in designing a newspaper type is to secure the maximum size of letter on the smallest size of body with the least waste of space between letters and words; while also preserving the right relation between the appearance of the letters and the length of the line to which they are set, and to increase, if possible, the ease of switching the eyes from the extreme right to the extreme left of the line [Morison, 1956].

Newspaper text proportions also derives its context from the **reading typeface** and legible **economic text setting**: news type in a legible **economic text setting** is often set at 8–10 point, set with 1–2 points of leading or even set solid (line height is the type size itself with no extra space between lines), with measures of typically 12ems accommodating 4–6 words. To balance economy and readability, the setting will have just enough interlinear space to be adequate for reading. The grey of text blocks set in this manner must balance with other elements of the **news typographic design**. The speed of news production prevents editors from fine-tuning all these parameters for each page.

#### 1.3.2.2 Solution

Use proportions that provide sufficient interlinear space to read easily when set solid. Letter widths should be narrow enough to fit an average of six words in the given measure while still being easy to read.

#### 1.3.2.3 Rationale

Economy and readability are the two primary, opposing forces in newspaper proportions. Economy drives increasing the number of lines per column-inch and characters per line, driving type to be set solid, and increasing the character density of each line.

Readability requires sufficient interlinear space to allow the eye to easily track from the end of a line to the beginning of the next. Meanwhile, a reader's perception of readability demands type that appears large.

Therefore, a balance must be struck: proportions to allow solid setting with readable interlinear space, while also having a high character density, without appearing crowded or dark, all while remaining readable.

#### 1.3.2.4 Implementation

A news typeface must have the greatest possible size and clearness of impression [Morison, 1932]. It must appear equally readable and have a comparable size to typefaces previously used by the publication.

Use proportions that are oblong, not square, [Hutt, 1960] and that have **economic widths** to fit the appropriate number of words per line. Use sufficiently high ascenders so that good interlinear spacing is built into the design [Morison, 1956]. Shortening descenders can create extra space. The proportions of these extenders must balance with the x-height so that letters have **large apparent size**. Figures 2 and 3 demonstrate this balance of extenders, x-height, and interlinear space.

Adjust serif dimensions to give the appropriate grey on the page. Serifs should taper because halation causes straight serifs to lose apparent length [Dawson and Farey, 2002].
