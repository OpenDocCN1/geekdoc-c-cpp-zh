# Figure 2.9 A Generic Frame for Property

| Slots | Fillers |
|---|---|
| name | property |
| specialization_of | a_kind_of object |
| types | (car, boat, house) if-added: Procedure ADD_PROPERTY |
| owner | default: government if-needed: Procedure FIND_OWNER |
| location | (home, work, mobile) |
| status | (missing, poor, good) |
| under_warranty | (yes, no) |

correspond to the expectations of a situation that we build up based on experience. When we encounter a new situation, the closest frame is modified to help us adjust to the situation. People do not start from scratch in every new situation. Instead, the defaults or other fillers are modified. Defaults are often used to represent commonsense knowledge. Commonsense knowledge can be considered to be the knowledge that is generally known. We use commonsense when no more situation-specific knowledge is available.

The if-added type is run for procedures to be executed when a value is to be added to a slot. In the types slot, the if-added procedure executes a procedure called ADD-PROPERTY to add a new type of property, if necessary. For example, this procedure would be run for jewelry, TV, stereo, and so forth since the types slot does not contain these values.

An if-removal type is run whenever a value is to be removed from a slot. This type of procedure would be run if a value were obsolete.

Slot fillers may also contain relations, as in the specialization of slots. The a-kind-of and is-a relations are used in Figures 2.9, 2.10, and 2.11 to show how these frames are hierarchically related. The frames of Figures 2.9 and 2.10 are generic frames while that of Figure 2.11 is a specific frame because it is an instance of the car frame. We have adopted the convention here that a-kind-of relations are generic and is-a relations are specific.

Frame systems are designed so that more generic frames are at the top of the hierarchy. It is assumed that frames can be customized for specific cases by modifying the default cases and creating more specific frames. Frames attempt to model real-world objects by using generic knowledge for the majority of an object's attributes and specific knowledge for special cases. For example, we commonly think of birds as creatures that can fly. Yet certain types of birds such as penguins and ostriches cannot fly. These types represent more specific classes