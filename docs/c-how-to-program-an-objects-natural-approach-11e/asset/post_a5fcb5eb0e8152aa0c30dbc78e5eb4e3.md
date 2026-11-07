
With the ability to process both text and image inputs.¹⁸¹ Powerful, large-language-model apps like ChatGPT and Google’s Bard¹⁸² sometimes produce incorrect results or “hallucinations,”¹⁸³ so you should verify the information tools like these provide.

When you converse with ChatGPT and similar tools, it may seem like you’re chatting with another person. In 1950, Alan Turing proposed the imitation game—now known as the Turing test—as a way to determine whether a computer exhibits intelligent behavior.¹⁸⁴ In it, three computer terminals would be hidden from one another, with two people operating terminals via text-based inputs and the third being computer-operated. One person would ask text-based questions that would be sent to the other two terminals. The second person and the computer would send text responses. If the person asking the questions could not determine whether the answers came from the other person or the computer, then the computer would be considered to have exhibited intelligent behavior.

### Dall-E 2

OpenAI’s Dall-E 2 is a generative AI for creating images from natural-language text prompts,¹⁸⁵ ¹⁸⁶ such as, “Generate an image of a golden retriever dog in the style of Claude Monet.” Visit https://labs.openai.com/ to view sample images created by Dall-E 2—hovering over an image reveals the text prompt on which the image is based. Some text prompts that have produced cool-looking images include:

- “An armchair in the shape of an avocado.”
- “A futuristic neon lit cyborg face.”
- “A van Gogh style painting of an American football player.”
- “A Formula 1 car driving on a neon road.”
- “A Shiba Inu dog wearing a beret and black turtleneck.”
- “A comic book cover of a superhero wearing headphones.”

### Checkpoint

1. **(Fill-In)** The ultimate goal of AI is to produce a(n) ________.

    **Answer:** artificial general intelligence.

2. **(Fill-In)** IBM’s Watson beat the two best human Jeopardy! players. Watson was trained using a combination of ________ learning and ________ learning techniques.

    **Answer:** machine, reinforcement.

## 1.17 Wrap-Up

This chapter introduced basic computer hardware, software and Internet concepts. We considered how computers are organized into logical units. We discussed Moore’s Law and noted that the continued improvements it so accurately predicted for many years seem to be ending. As a result, computer hardware designers have shifted to multi-core hardware architectures, which are programmed with the concurrent programming techniques we discuss in depth in Chapter 17, Parallel Algorithms and Concurrency: A High-Level View, and Chapter 18, C++20 Coroutines.

We showed how data items can be viewed as an organized hierarchy of increasingly complex types, from bits, to bytes, to fields, to records, to databases. We discussed the evolution of computer languages, from machine languages to assembly languages to high-level languages like C++, and we mentioned other popular high-level programming languages.

We considered popular desktop and laptop operating systems, including the proprietary Microsoft Windows and the open-source Linux. And we considered mobile operating systems, including Apple’s proprietary iOS for its iPhones and Google’s open-source Android that runs on a wide variety of smartphones from other vendors.

We encouraged you to avoid reinventing the wheel when developing new software and instead use existing software components from the C++ standard library and open-source C++ libraries, like Boost. We use Boost classes in two of our nine objects-natural case studies.

We presented a friendly introduction to object orientation using an automobile analogy to discuss classes, objects, inheritance and polymorphism. This provides the groundwork for our objects-natural case studies in Chapters 2 through 9 and our detailed treatment of the principles of object-oriented programming in Chapters 9–11, which are then used throughout the rest of the book.

We discussed a simplified view of a C++ development environment and the steps involved in C++ program development, including editing, preprocessing, compiling, linking, loading and executing. Between the software installation discussions in the Before You Begin section and the Test-Drives in Section 1.11, you installed the compiler(s) you’ll use to compile this book’s programs and the programs you write to solve the exercises.

We discussed the Internet, the World Wide Web, the Cloud and the Internet of Things (IoT). We introduced the Metaverse and associated technologies, including blockchain, cryptocurrencies, non-fungible tokens (NFTs), Web3, augmented reality (AR), virtual reality (VR) and mixed reality.

We considered various key software development technologies, including refactoring, design patterns, software development kits (SDKs), version control systems (VCS), agile software development, test-driven development (TDD), microservices and containerization.

We considered big data and various data sizes from megabytes to exabytes. Finally, we discussed artificial intelligence (AI)—an intersection between computer science and data science—introducing various AI technologies, including artificial general intelligence (AGI), machine learning and deep learning and reinforcement learning, and presenting various AI milestones, including generative AIs like ChatGPT and Dall-E 2. In Chapter 2, we begin our presentation of C++ programming.

## Exercises

- 1.1 Categorize each of the following items as either hardware or software:
    - a) CPU.
    - b) C++ compiler.
    - c) ALU.
    - d) C++ preprocessor.
    - e) input unit.
    - f) an editor program.

- 1.2 *(Computer Organization)* Fill in the blanks in each of the following statements:
    - a) The logical unit that receives information from outside the computer for use by the computer is the ________.
    - b) ________ is the logical unit that sends information the computer has already processed to various devices for use outside the computer.
    - c) ________ and ________ are the computer’s logical units that retain information.
    - d) ________ is the computer’s logical unit for performing calculations.
    - e) ________ is the computer’s logical unit for making logical decisions.
    - f) ________ is the computer’s logical unit for coordinating the other logical units’ activities.

- 1.3 Discuss the purpose of each of the following:
    - a) `cin`
    - b) `cout`
    - c) `cerr`

- 1.4 Fill in the blanks in each of the following statements:
    - a) Information in the computer’s memory unit is ________—it’s typically lost when the computer’s power is turned off.
    - b) As a measure of computer memory size, TB stands for ________—which is 1024 gigabytes.
    - c) Most computers today have ________ processors that economically implement multiple processors on a single integrated circuit chip.
    - d) ________ enable concurrent programming with a sequential like coding style.
    - e) The most popular database model is the ________ database in which data is stored in simple tables of rows and columns.
    - f) ________ is the process of searching through extensive collections of data to find valuable insights.
    - g) With ________ software individuals contribute to developing, maintaining and evolving the software. Anyone can then use that software for their own purposes—normally at no charge, but subject to various (typically generous) licensing requirements.
    - h) Today, most of the code for general-purpose operating systems is written in ________.
    - i) The C++ programming models are ________, ________, ________, ________, ________.
    - j) Existing older C++ code using older coding idioms is called ________ code.
    - k) When writing new software avoid ________. Instead use existing pieces from code libraries.
    - l) Microsoft’s primary language for the Metaverse is ______.
    - m) The ______ that objects come from are essentially reusable software components.
    - n) The protocol for communicating over the ARPANET became known as the ______.
    - o) TCP ensured that messages, consisting of sequentially numbered pieces called ______ were properly delivered from sender to receiver, arrived intact and were reassembled in the correct order.
    - p) In the Internet of Things (IoT) a “thing” is any device with a(n) ______ and the ability to send, and sometimes receive, data automatically over the Internet.
    - q) The applications-development methodology of ______ enables you to rapidly develop powerful software applications by combining (often free) complementary web services and various forms of information feeds.
    - r) ______ typically refers to simulated, 3D environments that you interact with.
    - s) ______ is a software-based ledger distributed over nodes on the Internet.
    - t) A ______ is a digital or virtual currency secured by cryptography.
    - u) ______ are blockchain-based “cryptographically unique tokens linked to digital or physical content, providing proof of ownership.”
    - v) ______ is by far the most widely used version control system.
    - w) The “four Vs” of big data are ______, ______, ______, and ______.
    - x) Some people feel that the ultimate problem to be solved in AI is ______.
    - y) ChatGPT is an example of the field of ______.

- 1.5 State which of the following are true and which are false. If false, explain why.
    - a) Computing costs are dropping rapidly due to impressive developments in hardware, software and Internet technologies.
    - b) For decades, computer power approximately doubled inexpensively every year. This remarkable trend is called Moore’s law.
    - c) Taking full advantage of multi-core architecture requires writing multithreaded applications.
    - d) Any computer can directly understand only its own assembly language.
    - e) The software that contains the core operating-system components is called the kernel.
    - f) iOS is the most widely used mobile-phone operating system.
    - g) C++ is the premier language for building high-performance business-critical and mission-critical operating systems.
    - h) The programming language most closely associated with the expression “write once, run anywhere” is Java.
    - i) Swift is widely used to add programmability to web pages, such as animations and user interactivity.
    - j) As the ARPANET evolved, to enable the huge variety of networking hardware and software to intercommunicate, ARPA developed the Internet Protocol (IP), which created a true “network of networks.”
    - k) Cloud computing allows you to increase or decrease computing resources to meet your needs at any given time.
    - l) IoT is an example of edge computing.
