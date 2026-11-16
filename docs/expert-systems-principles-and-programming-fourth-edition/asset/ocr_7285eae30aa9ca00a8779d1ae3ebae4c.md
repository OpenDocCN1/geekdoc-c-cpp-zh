is generally used for broad knowledge representation. Just as with semantic nets, there are no standards for defining frame-based systems. A number of special-purpose languages have been designed for frames, such as FRL, SRL, KRL, KEE, HP-RL, and frame enhancement features to LISP such as LOOPS and FLAVORS.

A frame is analogous to a record structure in a high-level language such as C or an atom with its property list in LISP. Corresponding to the fields and values of a record are the slots and slot fillers of a frame. A frame is basically a group of slots and fillers that define a stereotypical object. A frame for a car is shown in Figure 2.8. In OAV terms, the car is the object, the slot name is the attribute, and the filler is the value.

# Figure 2.8 A Car Frame

| Slots | Fillers |
| :--- | :--- |
| manufacturer | General Motors |
| model | Chevrolet Caprice |
| year | 1979 |
| transmission | automatic |
| engine | gasoline |
| tires | 4 |
| color | blue |

Most frames are not as simple as of the one shown in Figure 2.8. The utility of frames lies in hierarchical frame systems and inheritance. By using frames in the filler slots and inheritance, very powerful knowledge representation systems can be built. In particular, frame-based expert systems are very useful for representing causal knowledge because their information is organized by cause and effect. By contrast, rule-based expert systems generally rely on unorganized knowledge that is not causal.

Some frame-based tools such as KEE allow a wide range of items to be stored in slots. Frame slots may hold rules, graphics, comments, debugging information, questions for users, hypotheses concerning a situation, or other frames.

Frames are generally designed to represent either generic or specific knowledge. Figure 2.9 illustrates a generic frame for the concept of human property.

The fillers may be values, such as property in the name slot, or a range of values, as in the types slot. The slots may also contain procedures attached to the slots, called procedural attachments. These are generally of three types. The if-needed type is executed when a filler value is needed but none are initially present or the default value is not suitable. Defaults are of primary importance in frames because they model some aspects of the brain. Defaults