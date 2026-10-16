
![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_45_0.png)

## Chapter 6
### Text Usability

When we discuss design and usability, we tend to focus on visual elements first—text often gets overlooked. This is unfortunate, because text is one of the main ways in which people interact with your application or website. In fact, in tests that track the movement of people’s eyes as they scan a screen, text is often the first thing people look for.¹

> When asked for feedback on a web page, users will comment on the quality and relevance of the content to a much greater extent than they will comment on navigational issues or the page elements that we consider to be “user interface” (as opposed to simple information). Similarly, when a page comes up, users focus their attention on the center of the window where they read the body text before they bother looking over headerbars or other navigational elements.

The guys at 37signals concur. In Getting Real [FHL09], they write that “good writing is good design.” Words need to be considered as part of the interface design.

Have you ever tried buying a computer online, and instead of telling you in plain language what capabilities it has, the site lists a bunch of marketing buzzwords? Hmm...do I want the one with “MagSafe” or the one with “OneKey Theater” or the one with “One-button ThinkVantage” or the one with “Multi-Convergence UltraTouch Enterprise Panel Extensibility”? OK, I made the last one up, but the other ones are real.³

Words are how people interact with your product. Design is communication: if people don’t understand you, they can’t use your product.

Since words are used everywhere in your product, on your website, in your manuals, in the things you say when people interact with you personally, and even in the class names and comments in your code, it’s best to get them right early on.

But how do you know which words to use?

### 6.2 People Don’t Want to Read

This might sound strange coming after a section about the importance of text, but the hard truth is this: most people avoid reading whenever possible.

Merely by reading this book, you have proven that you are quite unlike most of your users. In 1987 in “Paradox of the Active User,”⁴ John M. Carroll and Mary Beth Rosson pointed out that “learners at every level of experience try to avoid reading.” Not much has changed in the last two decades. In fact, it may be getting worse: a 2007 study by the National Endowment for the Arts⁵ concluded that Americans are not just reading less than they used to, but they are also reading less well.

You have probably been on the receiving end of a “my printer has stopped working” call:

> **Friend:** I really need to print this document, but my printer just doesn’t work anymore.
> 
> **Me:** OK, what exactly happened?
> 
> **Friend:** I’m trying to print, but it doesn’t work.
> 
> **Me:** Did you get an error message?
> 
> **Friend:** *Oh, yes, an error popped up.*
> 
> **Me:** *What did it say?*
> 
> **Friend:** *How should I know? I just clicked it away, of course, but that didn’t fix the problem.*

A paper from the psychology department of the North Carolina State University titled “Failure to Recognize Fake Internet Popup Warning Messages”⁶ analyzed how people deal with fake pop-up warnings. When discussing the results, the researchers note:

Data from the post task questionnaire indicated that 12% of those who clicked on the OK button indicated that they did so because the text told them to, while 23% said they always click on that button when they encounter error messages. Just under half (42%) responded that they just wanted to “get rid of it.”

Pop-up windows don’t even consciously register with people before they click them away. They are just a nuisance that keeps people from doing their work, and making them go away usually seems to fix the problem.

But this doesn’t just apply to text in pop-up messages. People skip text whenever they think they can get away with it.

### 6.3 Say Less

Since people don’t read, it’s best to avoid bothering them with text whenever possible.

For example, don’t warn people when they are about to do something destructive. Instead, allow them to undo their change.

Similarly, if an error occurs and you have a way to make your product recover on its own without telling the user, do it. If the user has entered a website address that is truncated but your website receives enough information to identify the page he’s looking for, simply forward him to that page. If your application tries to connect to a server but the connection times out, make the application try again before telling the user there’s something wrong. Notify the user only if your product really can’t fix the problem on its own.

If people don’t understand some part of your user interface, don’t add explanatory text. This just adds more clutter and makes the problem worse.

If it’s impossible to avoid communicating, design your user interface under the assumption that people won’t read what you write. For example, use verbs as button labels, and make sure that each button has a specific, mutually exclusive label. Instead of labeling two buttons “Yes” and “No,” label them “Delete File” and “Cancel.” That way, people don’t have to read the text in the dialog box to figure out what each button does.

6. Read it at http://media.haymarketmedia.com/Documents/1/SharekWogalterFakeWarning_publicationFinal_805.pdf.

### 6.4 Make Text Scannable

Often you can’t avoid text. To know how to write, first you need to know how people read.

Jakob Nielsen’s research shows that people typically don’t read text on the Web word by word. Instead, they “scan” the page, looking for sentence fragments that contain what they are looking for. To help people do that, Nielsen suggests⁷ the following rules:

- Use words that make sense to your audience.
- Convey one idea in each paragraph.
- Introduce the paragraph’s idea in the first sentence so people can quickly decide whether to read the paragraph.
- Use meaningful headings.
- Highlight keywords.
- Use bullet lists.
- Keep text short, simple, and informal.
- Start text with conclusions, and include a summary of its content.

### 6.5 No Fluff

People are trying to achieve a goal and are reading your text because they think it might help them with their task. Write short, clear, obvious sentences. Keep individual paragraphs short. Don’t waste your readers’ time. Keep their goal in mind.

As Patricia Wright puts it in the book *Quality of Technical Documentation* [SJ94], “Writers often believe that they should communicate more than readers want to know.”

When you’re writing, ask yourself, “Does this sentence help the user?” If it doesn’t, get rid of it.

### 6.6 Sentences Should Have One Obvious Interpretation

Avoid sentences that can be interpreted in two different ways and sentences that lure your readers into an improper understanding when they have read only part of them.⁸

Readers try to make sense of sentences before they reach the period at the end. Some sentences can mislead the reader. Consider the first few words of this headline:⁹

> “Burger King fries the holy grail…”

Now why would Burger King fry the holy grail? The sentence’s meaning becomes clear when you finish reading it:

> “Burger King fries the holy grail for potato farmers”

Ah, the fries *are* the holy grail. It’s still not entirely unambiguous, but the meaning is reasonably obvious now.

Reading such a sentence requires more work on the part of your readers, since they’re forced to backtrack if they start with a wrong interpretation. To avoid confusing them, ask yourself whether a sentence is unambiguous even if you’ve read only part of it. A simple change makes this sentence completely clear:

> “Burger King fries are the holy grail for potato farmers”

Can you spot the problem with the following sentence?

8. These are often called garden-path sentences, from the saying “to be led up the garden path.” The intuitive understanding of such a sentence is misleading; reaching the end of the sentence forces the reader to backtrack, looking for a different interpretation. Wikipedia has more on the topic: http://en.wikipedia.org/wiki/Garden_path_sentence.

9. I found this example via the excellent Language Log blog at http://languagelog.ldc.upenn.edu/nll/?p=1762. Language Log is definitely worth reading if you’re interested in writing.

7. You can find a collection of Nielsen’s essays on this topic at this address: http://www.useit.com/papers/webwriting/.
