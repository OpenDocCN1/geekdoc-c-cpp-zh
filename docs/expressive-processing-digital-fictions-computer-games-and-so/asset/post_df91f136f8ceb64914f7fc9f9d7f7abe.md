
historical narrative will be produced for that audience by Terminal Time’s mechanisms. This is followed by the first question period, in which “an initial ideological theme (from the set of gender, race, technology, class, religion) and a narrative arc (e.g. is this a progress or decline narrative) are established” (Mateas, Vanouse, and Domike 2000). The next stage is the generation and presentation of the part of story covering the years 1000-1750 CE, which takes six minutes. Following this, a second set of questions refines the ideological theme chosen in the first set and may introduce a subtheme (e.g., race with a subtheme of class, or technology with religion). The next section of the story is then generated and presented, covering roughly 1750–1950 CE, and again taking six minutes. This is followed by a final set of questions that further refines theme(s) and introduces the possibility for a reversal (e.g., a decline narrative may become a progress one). This is followed by the generation and presentation of the last phase of the story, covering roughly 1950 CE to the end of the millennium.

As each phase of storytelling takes place, the ideological models not only become further shaped by the audience responses but also more blunt in their operations. This, combined with audiences’ greater familiarity with more recent history, causes the exaggerated ideological spin of the story to become steadily more apparent over the twenty minutes of a Terminal Time performance. Toward the end of performances this culminates in story fragments such as the glowing description of the Chinese invasion of Tibet quoted above. In that particular case, the ideological goals at work were those that Terminal Time’s creators refer to as belonging to the “anti-religious rationalist.”

The representation of ideology in Terminal Time is based on that developed for the Politics system—which itself was a successor to the ideology machine created by Robert Abelson and his collaborators in the 1950s through 1970s (and discussed in chapter 4). In Terminal Time ideology is represented as a set of goal trees—specifically, rhetorical goals for what the story will demonstrate through its history of the millennium. While the initial audience polling produces one of the goal trees originally crafted by Terminal Time's authors, further questioning may add, delete, or change goals. For example, during the second round of questioning a subtheme may be introduced via the combination of goals from one tree with another.

Below is an instance of Terminal Time authoring—specifically, the antireligious rationalist goal tree as it exists before any modifications. Notice that because “show-thinkers-persecuted-by-religion” is a subgoal of both high-level goals, it can satisfy both of them.

```
show-religion-is-bad
show-religion-causes-war
show-religion-causes-crazy-self-sacrifice
show-religion-causes-oppression
show-religion-causes-self-abuse
show-thinkers-persecuted-by-religion
show-halting-rationalist-progress-against-religion
show-thinkers-opposing-religious-thought
show-thinkers-persecuted-by-religion
(Mateas, Vanouse, and Domike 2000, 239)
```

In their paper, Mateas, Vanouse, and Domike write that in Terminal Time, “nine major ideologues are represented using a total of 222 rhetorical goals.” The authors of Terminal Time represent the crafting of these ideological models as authoring, as the creation of an artwork. But this is not always the way that their work is understood in the AI community. As Mateas reports:

The first time I presented Terminal Time to a technical audience, there were several questions about whether I was modeling the way that real historians work. The implicit assumption was that the value of such a system lies in its veridical model of human behavior. In fact, the architectural structure of Terminal Time is part of the concept of the piece, not as a realist portrait of human behavior, but rather as a caricature of certain institutionalized processes of documentary film making, (2002, 57–58)

This reception of Terminal Time should perhaps come as no surprise, given my earlier discussion of anthropomorphized models within AI. And for understanding Terminal Time and the ideas that motivate it, one does need to consider how human models of history and ideology interact with the system. Yet the place to look for human models is not within the system itself. Rather, Terminal Time depends on the existence of these models in a very anthropomorphic location: within the audience.

## Event Knowledge

In order for Terminal Time events to be accessible to the system, they need to be represented in a formalized manner. The Terminal Time approach to this problem involves building on top of a representation of everyday knowledge called the “Upper Cyc Ontology” (an ambitious, in-process attempt to address the fundamental issues discussed earlier in the context of Minstrel). For Terminal Time’s purposes, the approach taken by the Cyc Ontology both structures how its own terms will be authored (as assertions in a knowledge base that also includes the terms from Upper Cyc and provides the lower-level grounding on top of which its terms are defined).

Terminal Time's historical events cover a range of levels of abstraction. They include, for example, the First Crusades, the invention of Bakelite, and the rise of Enlightenment philosophy. Here is an example of how events are authored for Terminal Time. Specifically, this is the representation of one event, the Giordano Bruno story:

```
:: Giordano Bruno
(Sisa %GiordanoBrunoStory %HistoricalEvent)
(Sisa %GiordanoBrunoStory %IdeaSystemCreationEvent)
(Sisa %GiordanoBrunoStory %Execution)
(%circa %GiordanoBrunoStory (%DateRangeFn
  (%CenturyFn 16) (%CenturyFn 17)))
(SevenOccursAt %GiordanoBrunoStory
  SContinentOfEurope)
(SperformedBy %GiordanoBrunoStory %GiordanoBruno)
(SoutputsCreated %GiordanoBrunoStory
  %GiordanoBrunoIdeas)
(Sisa %GiordanoBrunoIdeas
  SPropositionalInformationThing)
(Sisa %GiordanoBrunoIdeas SSomethingExisting)
(%conflictingMOs %GiordanoBrunoIdeas
  %MedievalChristianity)
(Sisa %GiordanoBrunoIdeas %IdeaSystem)
(SperformedByPart %GiordanoBrunoStory
  %TheRomanCatholicReligiousOrg)
(SubjectActedOn %GiordanoBrunoStory
%GiordanoBruno)
(Mateas, Vanouse, and Domike 2000, 238)
```

In the above representation, terms preceded by a "%" are defined in the Upper Cyc Ontology, while those terms not preceded by "%" are defined within the Terminal Time ontology in terms of the Upper Cyc Ontology. An English-language gloss of this event representation reads:

The Giordano Bruno story, a historical event occurring in the 16th and 17th century, involved the creation of a new idea system and an execution. The idea system created in this event conflicts with the idea system of medieval Christianity. Both Giordano Bruno and a portion of the Roman Catholic Church were the performers of this event. Giordano Bruno was acted on (he was executed) in this event. (ibid.)

In order for a Terminal Time ideologue to make use of such an event, it must be possible to determine that the event can spin to support one of the current rhetorical goals. The Terminal Time system identifies candidate events by testing them for applicability. These tests are carried out through an “inference engine” written in Lisp. Here is the test for “show-thinkers-persecuted-by-religion”:

```
(%and
  (Sisa ?event %IdeaSystemCreationEvent)
  (Sisa ?event %Execution)
  (OutputsCreated ?event ?newIdeas)
  (%conflictingMOs ?newIdeas ?relBeliefSystem)
  (Sisa ?relBeliefSystem $Religion))
(ibid., 239)
```

As Mateas, Vanouse, and Domike point out, this is not any sort of general test for finding all instances of thinkers being persecuted by religion. For example, it assumes executions are the only type of persecution. Similarly, Terminal Time's representation of the Giordano Bruno story is not the only possible one. The Terminal Time authors note that in other circumstances, it might be desirable to represent Bruno's writings and execution as separate events, rather than one compound event.

But again, Terminal Time is not trying to create a realistic simulation of the behavior of historians or create a system that “really understands” history, or itself be a creative system. It is instead an authored artwork.

If the authors desired—at some point—for the system to be able to identify instances of religious groups persecuting thinkers that do not involve executions, in order to employ these events in its stories, then the test could be broadened to match the new class of events. As of 2000, the authors report that the system includes “134 historical events and 1568 knowledge base assertions” (beyond those assertions in the Upper Cyc Ontology). Given that all the possible examples of events involving religious persecution of thinkers (among that 134) also include executions, a broader test is not needed. But anyone involved in authoring historical event data for Terminal Time must do so with an awareness of the tests that will evaluate them later. In fact, it would make no sense to author historical events except in relation to the tests currently in the Terminal Time system, as events matching no tests would never be employed in stories. The authoring of events is thus tightly coupled to the authoring of tests.
