
Various Pex4Fun users posted their comments on the Internet to express their enthusiasm and interest (even addiction) to Pex4Fun. Here we included some examples:

> Pex4Fun could become a better FizzBuzz than FizzBuzz.
> it really got me 'excited'. The part that got me most is about spreading interest in/teaching CS: I do think that it's REALLY great for teaching—learning!

> Frankly this is my favorite game. I used to love the first person shooters and the satisfaction of blowing away a whole team of Noobies playing Rainbow Six, but this is far more fun.
>
> Teaching, learning—isn't this really the same, in the end? In fact, for me personally, it's really about leveraging curiosity, be it mine or someone else's—at best both! And Pex4Fun (+ all the stuff behind) is a great, promising platform for this: you got riddles, you got competition, you get feedback that makes you think ahead...
>
> I'm afraid I'll have to constrain myself to spend just an hour or so a day on this really exciting stuff, as I'm really stuffed with work.

> Pex4Fun improves greatly over Project Euler w.r.t. how proposed solutions are verified; in fact what it adds is that you don't just get a 'nope' but something more articulate, something you can build on. That's what I think is really great and exciting—let's push it even further now!

### 5.3.5 Code Hunt

Code Hunt [28,29] is a recent gaming platform evolved from Pex4Fun. Code Hunt includes more gaming aspects to offer more engaging experiences to the player. Figure 5.4 shows the main page of the Code Hunt website. The gaming platform also has sounds and a leaderboard to keep the player engaged.

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_146_0.png)

FIGURE 5.4 (See color insert.) The main page of the Code Hunt website.

With coding duels as the game type, Code Hunt organizes games in a series of worlds, sectors, and levels, which become increasingly challenging. Figure 5.5 shows the example list of sectors available for the player to choose from. In each level, a coding duel game is played by the player, who has to discover a secret code fragment and write code (in Java or C#) for it. Figure 5.6 shows an example coding duel for the player to play, with the player's code shown on the left-hand side of the figure. After the player clicks the Capture Code button (shown near the middle-top part of the figure, with the same effect of clicking the Ask Pex! button in Pex4Fun), the underlying Pex tool gives customized progress feedback to the player via the generated test cases, as displayed in the table on the right-hand side of Figure 5.5. In addition, Code Hunt might hint a user to focus on a particular line of code, as shown in the last line of the table on the right-hand side of the figure. When the player's code achieves the same result as the secret implementation, Code Hunt flashes Captured Code and provides a score to the player based on how good the code was. Other improvements for Code Hunt beyond Pex4Fun are that Code Hunt offers Java as a supported language (via a source code translator) and it runs on Microsoft Azure, making it scalable to a large number of simultaneous users.

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_146_1.png)

FIGURE 5.5 Example sectors in Code Hunt.

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_147_0.png)

FIGURE 5.6 (See color insert.) An example coding duel in Code Hunt.

## 5.4 DISCUSSION

Educational software engineering is closely related to the field of educational games [30] (i.e., games for education), with example conferences such as the Games+Learning+Society Conference (http://www.gameslearning-society.org/conference) and example initiatives such as the MacArthur Digital Media and Learning initiative (http://www.macfound.org/programs/learning). The field of educational games typically focuses on gaming technologies for supporting educational purposes, whereas educational software engineering typically focuses on software engineering technologies for supporting educational purposes. In the context of Pex4Fun and Code Hunt, the field of educational games would focus more on the aspect of gaming (Section 5.3) whereas the field of educational software engineering would focus more on the aspect of software engineering technologies (Section 5.3.1). Note that educational software engineering deals with not only educational games but also other educational tools not being games.

In addition, it is reasonable to consider that software engineering for developing educational games or generally educational tools (such as software quality assurance for educational game software) would be part of educational software engineering. In other words, educational software engineering is not limited to software engineering technologies as infrastructure support for educational tools (as exemplified by Pex4Fun and Code Hunt) and can also include software engineering tools or processes to assist the development of educational tools.

We advocate educational software engineering to be within software engineering research and to contribute to software engineering research in three example ways:

- 1. First, when targeting educational tasks, researchers may be able to leverage or develop software engineering technologies (to be effective for such tasks), which generally may not be effective or mature enough to deal with tasks related to software industry. An example case would be developing program synthesis technologies for educational tasks [5–7]. Another example case would be developing test generation technologies for Pex4Fun and Code Hunt, because secret implementations created for coding duels tend to be simpler than real-world code implementations.
- 2. Second, targeting at educational tasks may pose unique requirements for software engineering technologies. For example, test generation for software engineering tasks such as achieving code coverage aims at generating and reporting test inputs that can achieve new code coverage. However, test generation for Pex4Fun and Code Hunt aims at generating and reporting test inputs that can serve as feedback to achieve effective learning purposes.
- 3. Some educational tasks (such as intelligent tutoring [14] and problem generation [5–7]) call for creation of new software engineering technologies, which may not exist in traditional software engineering (because there are no counterparts in the software engineering domain for such tasks in the education domain).

## 5.5 CONCLUSION

In this chapter, we have defined and advocated educational software engineering as an emerging subfield of software engineering. Educational software engineering develops software engineering technologies for general educational tasks. In this subfield, gaming technologies often play an important role together with software engineering technologies. We have presented Pex4Fun (along with Code Hunt), one of our recent examples on leveraging software engineering and gaming technologies for teaching and learning programming and software engineering skills. Pex4Fun and Code Hunt can also be used in the context of MOOCs to address issues such as automatic grading.

## ACKNOWLEDGMENT

We thank the reviewers for their valuable feedback. Tao Xie’s work is supported in part by a Microsoft Research Award, NSF grants CCF-1349666, CNS-1434582, CCF-1434596, CCF-1434590, and CNS-1439481, and the NSF of China, number 61228203.

## REFERENCES

- 1. Mary Shaw. Software engineering education: A roadmap. In *Proceedings of FOSE*, pp. 371–380, Limerick, Ireland, 2000.
- 2. Mary Jean Harrold. Testing: A roadmap. In *Proceedings of FOSE*, pp. 61–72, Limerick, Ireland, 2000.
- 3. Dongmei Zhang, Yingnong Dang, Jian-Guang Lou, Shi Han, Haidong Zhang, and Tao Xie. Software analytics as a learning case in practice: Approaches and experiences. In *Proceedings of MALETS*, pp. 55–58, Lawrence, KS, 2011.
- 4. Dongmei Zhang, Shi Han, Yingnong Dang, Jian-Guang Lou, Haidong Zhang, and Tao Xie. Software analytics in practice. Special Issue, *IEEE Software*, 30(5):30–37, 2013.
- 5. Erik Andersen, Sumit Gulwani, and Zoran Popovic. A trace-based framework for analyzing and synthesizing educational progressions. In *Proceedings of CHI*, pp. 773–782, Paris, France, 2013.
- 6. Sumit Gulwani, Vijay Korthikanti, and Ashish Tiwari. Synthesizing geometry constructions. In *Proceedings of PLDI*, pp. 50–61, San Jose, CA, 2011.
- 7. Rohit Singh, Sumit Gulwani, and Sriram Rajamani. Automatically generating algebra problems. In *Proceedings of AAAI*, Toronto, ON, 2012.
- 8. Tao Xie, Suresh Thummalapenta, David Lo, and Chao Liu. Data mining for software engineering. *IEEE Computer*, 42(8):35–42, 2009.
- 9. Ahmed E. Hassan. The road ahead for mining software repositories. In *Proceedings of FoSM*, pp. 48–57, Beijing, China, 2008.
- 10. Armando Fox and David Patterson. Crossing the software education chasm. *Communications of the ACM*, 55(5):44–49, 2012.
- 11. Ken Masters. A brief guide to understanding MOOCs. *The Internet Journal of Medical Education*, 1, 2011. https://ispub.com/IJME/1/2/10995. doi:10.5580/1f21.
- 12. Rishabh Singh, Sumit Gulwani, and Armando Solar-Lezama. Automated feedback generation for introductory programming assignments. In *Proceedings of PLDI*, pp. 15–26, Seattle, WA, 2013.
- 13. Nikolai Tillmann, Jonathan De Halleux, Tao Xie, Sumit Gulwani, and Judith Bishop. Teaching and learning programming and software engineering via interactive gaming. In *Proceedings of ICSE, Software Engineering Education (SEE)*, pp. 1117–1126, San Francisco, CA, 2013.
