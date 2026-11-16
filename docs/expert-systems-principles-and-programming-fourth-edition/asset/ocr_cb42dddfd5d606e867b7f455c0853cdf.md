a given situation. That is, the fillers are procedures to perform some actions, such as removing a defective part from a conveyor belt. An action frame represents procedural knowledge. The combination of situational and action frames can be used to describe cause-and-effect relationships in the form of causal knowledge frames.

Very sophisticated frame systems have been built for a variety of tasks. One of the most impressive systems that demonstrated the power of frames to creatively discover mathematical concepts was the Automated Mathematician (AM) of Doug Lenat. The classic AM system of Lenat made conjectures of interesting new concepts and explored them. It came up with some completely new mathematical proofs of certain theorems. Many other examples of theorem provers and discovery systems are shown in Appendix G for this chapter.

# 2.10 DIFFICULTIES WITH FRAMES

Frames were originally conceived of as a paradigm for representing stereotyped knowledge. The important characteristic of a stereotype is that it has well-defined features so that many of its slots have default values. Mathematical concepts are good examples of stereotypes well suited to frames. The frame paradigm has an intuitive appeal because its organized representation of knowledge is generally easier to understand than either logic or production systems with many rules (Jackson 99).

However, major problems have appeared in frame systems that allow unconstrained alteration or cancellation of slots. The classic example of this problem is illustrated with a frame describing elephants, as shown in Figure 2.12.

# Figure 2.12 Elephant Frame

| name | elephant |
| specialization_of | a-kind-of mammal |
| color | grey |
| legs | 4 |
| trunk | a cylinder |

At first sight, the elephant frame seems like a reasonable generic description of elephants. However, suppose there exists a specific, three-legged elephant called Clyde. Clyde may have lost a leg due to a hunting accident or simply lied about losing a leg to get his name in this book. The significant thing is that the elephant frame claims that an elephant has four legs, not three. Thus we cannot consider the elephant frame to be the valid definition of an elephant.