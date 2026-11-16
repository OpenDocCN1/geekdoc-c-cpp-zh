usage and update frequency will decline. Ultimately, this leads to a fatal undermining of the whole process, and so it is extremely important to maintain ease-of-use for all the team.

![](bbox=[0.16, 0.2, 0.9, 0.54])

**FIGURE 6.8.1** *An example attack tree with 1 root, 3 child nodes, and 1–5 grandchildren.*

Most nontrivial systems usually have multiple independent attack-trees making up the complete Threat Model; there is no need to rigidly constrain yourself to a single tree that contains every attack (this would often require painful coercion of the attack descriptions).

# ## Security Policy: Nullifying Threats

The Security Policy is derived from the Threat Model. It explains how to counteract every potential threat, thereby rendering the system secure. Without a specific Threat Model, a Security Policy is largely useless, since it has become a solution without a precisely defined problem, no longer knowing the answer to: Secure from whom [Schneier03]?

Unlike the TM, the SP's purpose is to specify what the system and its administrators must do. It describes what they do, how they do it, and—where applicable—even why they do it. It must be precise; a vague SP creates ambiguity, which in turn is an opportunity for your team to accidentally create loopholes, or gaps between the secure elements, which will later be discovered and used by attackers.