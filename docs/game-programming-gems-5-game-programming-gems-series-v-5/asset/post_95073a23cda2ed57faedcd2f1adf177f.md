
can efficiently handle all the possible word permutations from a given dictionary. This reality suggests the need for constant, vigilant human intervention.

## Human Intervention

After all this technology, there's still the major concern that none of these tactics will fully provide a "safe," family-friendly environment. The fact is, any one or combined approach to filtering that fits within reasonable CPU/memory constraints will have easy workarounds.

Unfortunately, the best one can hope for is to make a reasonable effort from a technology standpoint, and hope that it covers a large majority of potential violators. But this technology will fail under many cases. If the game is still likely to suffer heavy abuse despite these safeguards, there is often no choice but to add a layer of human intervention. There are two often-used methods that help weed out a large majority of the worst-case users: the in-game supervisors and player feedback.

## In-Game Supervision

In-game supervision refers to an actual moderator or team of moderators, who actively play and patrol the online game, basically looking for any sort of violation. These moderators may choose whether to be listed as administrators, versus serving "undercover." While the consequences for bad behavior may include a ban from future play, often a looser punishment might solve the problem (for instance, a 30-day ban on chatting).

## Player Feedback

Player feedback can be quite powerful if handled correctly. With this technology, the other players themselves have a means to report unruly behavior. This allows the community to actively police themselves and potentially weed out more cases of unwanted actions than a team of moderators could hope to find. While this still requires people to read the feedback and act accordingly, as well as handle cases of fraudulent feedback, this also allows more active reporters to become "senior" members of the community, and likely will serve as the game's staunchest advocates.

## Conclusion

This article discussed a couple of different ways to implement vulgarity filtering in an online game. Further, this article talked about ways in which this filtering can—and will—fail, and where human intervention is still necessary. Fortunately, the methods discussed here will severely blunt the blow of a malicious user, to the point where it may become too difficult or frustrating for the user to try and continue his bad behavior. Between combinations of these methods, users can be assured of a safer, protected game environment.

## References

- [Fcproject01] The Free Expression Policy Project. “Fact Sheet on Internet Filtering.” Available online at http://www.fepproject.org/factsheets/filtering.html.
- [IGN01] IGN Xbox. “Xbox Live Etiquette.” Available online at http://xbox.ign.com/articles/377/377569p1.html.
- [Oreilly01] O’Reilly Network. “XML.com: XML from the Inside Out.” Available online at http://www.xml.com/.
- [Xerces01] “Xerces C++ Parser.” Available online at http://xml.apache.org/xerces-c/.

## Fast and Efficient Implementation of a Remote Procedure Call System

Hyun-jik Bae
imays@hitel.net

There are many articles on network game development focused on aspects such as dead reckoning, distributed game servers, throttling, load balancing, smart seeds, and so on. These are very useful and important ideas and can be applied to many projects. All these techniques share a common characteristic in that they all require sending and receiving at least one message; this code is typically one of the greatest sources of redundant network code.

Many network game programmers tend to write redundant code that treats every network message the same but could easily be consolidated. Sending and receiving messages involves many switch-case statements and structure definitions. This redundancy only grows as messages are added or changed during the development process.

This article introduces a solution to reduce this burden, focusing on a code-level perspective.

First, let’s take a look at a typical problem area for most network games. Listing 6.4.1 shows an example that processes two messages: “move knight” and “attack enemy.”

### Listing 6.4.1 Our Familiar Networking Code

```cpp
//////// on both sides
#define Message_Knight_Move_ID 12
#define Message_Knight_Attack_ID 13

struct Message
{
    int m_msgID;
};

struct Message_Knight_Move:public Message
{
    int m_id;
    float m_x,m_y,m_z;
};

struct Message_Knight_Attack:public Message
{
    int m_id;
    int m_target;
    int m_damage;
};
```

////////// on sender side

```cpp
void Knight_Move(int id,float x,float y,float z)
{
    Message_Knight_Move msg;
    msg.m_msgID=Message_Knight_Move_ID;
    msg.m_id=id;
    msg.m_x=x;
    msg.m_y=y;
    msg.m_z=z;
}

void Knight_Attack(int id,int target,int damage)
{
    Message_Knight_Attack msg;
    msg.m_msgID=Message_Knight_Attack_ID;
    msg.m_id=id;
    msg.m_target=target;
    msg.m_damage=damage;
}

void DoReceivedMessage(Message* msg)
{
    switch(msg->m_msgID)
    {
    case Message_Knight_Move_ID:
    {
        Message_Knight_Move* msg2=
        (Message_Knight_Move*)msg;
    }
    Do_Knight_Move(
        msg2->m_id,
        msg2->m_x,
        msg2->m_y,
        msg2->m_z);
    break;
    // cases for other message types
    case Message_Knight_Attack_ID:
    {
        Message_Knight_Attack* msg2=
        (Message_Knight_Attack*)msg;
    }
    Do_Knight_Attack(
        msg2->m_id,
        msg2->m_target,
        msg2->m_damage);
    break;
    // ... cases for other message types
    }
}
```

Let's now assume a case where we must add another message type. We must modify four spots in Listing 6.4.1 for the new message: a new message ID, a new message structure, a new function sending the message, and a new case for reading the message. This cumbersome work can be reduced by using streaming classes, such as Carchive or std::istream, or by writing your own. With these classes, Listing 6.4.1 can be simplified to look like Listing 6.4.2.

### Listing 6.4.2 Another Style of Our Familiar Networking Code

```cpp
////////// on both sides
#define Message_Knight_Move_ID 12
#define Message_Knight_Attack_ID 13

////////// on sender side
void Knight_Move(int id,float x,float y,float z)
{
    Message msg;
    msg<<(int)Message_Knight_Move_ID;
    msg<<id<<x<<y<<z;
}

void Knight_Attack(int id,int target,int damage)
{
    Message msg;
    msg<<(int)Message_Knight_Attack_ID;
    msg<<id<<target<<damage;
}

////////// on receiver side
void DoReceivedMessage(Message* msg)
{
    int msgID;
    (*msg)>>msgID;
    switch(msgID)
    {
    case Message_Knight_Move_ID:
    {
        int id;
        float x,y,z;
        (*msg)>>id>>x>>y>>z;
        Do_Knight_Move(id,x,y,z);
    } break;
    case Message_Knight_Attack_ID:
    {
        int id,target,damage;
        (*msg)>>id>>target>>damage;
        Do_Knight_Attack(id,target,damage);
        break;
        // ... cases for other message types
    }
    }
}
```

Either way, we can send, receive, and process messages by calling Knight_Move() on the send side and doing Do_Knight_Move() on the receiver side, as well as the messages Knight_Attack() and Do_Knight_Attack().

Notice the pattern in these examples, in that they're very redundant. They can be abstracted for now to just read as one-line declarations, such as Listing 6.4.3, which is the goal for how we want our actual game code to look.

```cpp
Knight_Move(int id,float x,float y,float z);
Knight_Attack(int id,int target,int damage);
```
Listing 6.4.3 The ultimate style we desire

We can refer to Listings 6.4.1 and 6.4.2 as the manual send-receive-switch-case code and refer to Listing 6.4.3 as the automatic send-receive-switch-case code. Later in this gem, we'll discuss how these send-receive-switch-case codes can be generated automatically, which is one of the major benefits of Remote Procedure Calls (RPC).

## RPC: Introduction

RPC is a message-passing facility that is independent of the underlying network layer and allows a distributed application to call services available on various computers in that network. Put more simply, RPC abstracts the technique of a program on one computer requesting a function call on another computer. For a complete introduction to generic RPC usage, refer to an operating system textbook (Silberschatz02).

There are many RPC implementations, some available by several major companies. Some of the more well known are MS-RPC, DEC-RPC, DCOM, CORBA, and Java RMI. (DCOM, CORBA, and Java RMI have object-oriented behavior, but their concepts are also based on RPC.) In this article, let's call these implementations legacy RPC systems. Legacy RPC systems are stable and support many features such as security, authentication, and many protocol compatibilities. However, because many of these implementations have some drawbacks for game programming, we want to write our own RPC system and avoid the following problems with legacy RPC:

- Hard to understand and use
- Too redundant and cumbersome for game applications
