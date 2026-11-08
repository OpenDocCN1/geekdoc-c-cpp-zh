
Don’t get me wrong. When team members work from home, there is still a significant loss of nonverbal communication. Serendipitous conversations are much rarer. No matter how electronically connected the team is, they are still not together in the same space. This puts the people working from home at a distinct disadvantage. There are always conversations and impromptu meetings that they miss. Despite the vast data bandwidth they may enjoy, they are still communicating through a peephole compared to those who are co-located.

A team that is mostly co-located but has a member or two who work from home one or two days per week will likely not notice any significant impediment, especially if they have invested in some good, high-bandwidth remote-communication tools.

On the other hand, a team composed of people who work almost entirely from home will never work as well as a team that is co-located.

Don’t get me wrong. In the early ’90s, my partner Jim Newkirk and I successfully managed a team that had no co-location at all. Everyone worked entirely from home. We met in person twice per year at most, and some of us lived in different time zones. On the other hand, we all spoke the same language, shared the same culture, and our time zones were never more than two hours apart. We made it work. We made it work very well. But it would have worked even better if we’d been together in the same room.

## Conclusion

At the Snowbird meeting in 2000, Kent Beck said that one of our goals was to heal the divide between business and development. The business-facing practices play a big role in satisfying that goal. By following these practices, business and development have a simple and unambiguous way to communicate. That communication breeds trust.

## TEAM PRACTICES

![](img/8facf878fd02eafcdb1e1193ad5963b0_123_0.png)

## SMART FACTORY & INDUSTRY 4.0

### Manufacturing Reimagined

Smart Factory uses Internet of Things (IoT), Artificial Intelligence (AI), and robotics to create a self-optimizing manufacturing environment. Factories become intelligent, connected, and efficient.

From smart sensors tracking every movement to AI predicting maintenance needs, the smart factory revolution is here. Real-time data flows through the entire production line, enabling smarter decisions, reducing waste, and increasing profitability.

![](img/8facf878fd02eafcdb1e1193ad5963b0_125_0.png)

- **IoT-Connected Equipment**
- **AI-Driven Analytics**
- **Predictive Maintenance**
- **Automated Robotics**

Industry 4.0 is not just about automation—it is about creating a digital ecosystem. The smart factory integrates cyber-physical systems, cloud computing, and the Internet of Things to enable real-time monitoring and control. With these technologies, manufacturers can respond instantly to market changes, customize products at scale, and achieve unprecedented operational efficiency.

been given to the *Metaphor* practice. What the team needs is a model of the problem domain, which is described by a vocabulary that everyone agrees on. And I mean *everyone*—the programmers, QA, managers, customers, users… *everyone.*

In the 1970s, Tom DeMarco called such models *Data Dictionaries.*³ They were simple representations of the data manipulated by the application and the processes that manipulated that data. Evans greatly amplified the simple idea into a discipline of modeling the domain. Both DeMarco and Evans use those models as vehicles to communicate with all of the stakeholders.

As a simple example, I recently wrote a video game called SpaceWar. The data elements were things like Ship, Klingon, Romulan, Shot, Hit, Explosion, Base, Transport, etc. I was careful to isolate each of these concepts into their own models and to use those names exclusively throughout the application. Those names were my Ubiquitous Language.

The Ubiquitous Language is used in all parts of the project. The business uses it. The developers use it. QA uses it. Ops/DevOps use it. Even the customers use those parts of it that are appropriate. It supports the business case, the requirements, the design, the architecture, and the acceptance tests. It is a thread of consistency that interconnects the entire project during every phase of its lifecycle.⁴

## Sustainable Pace

> “The race is not to the swift…”
>
> — Ecclesiastes 9:11
>
> “…But he who endures to the end will be saved.”
>
> — Matthew 24:13

3. DeMarco, T. 1979. *Structured Analysis and System Specification.* Upper Saddle River, NJ: Yourdon Press.

4. “It’s an energy field created by all living things. It surrounds us and penetrates us. It binds the galaxy together.” Lucas, G. 1979. *Star Wars: Episode IV—A New Hope.* Lucasfilm.

## OVERTIME

You’d think that I would have learned my lesson from that experience. But, of course, I did not. Over the next 20 years, I continued to work long hours for my employers. I continued to fall for the *important project* meme. Oh, I didn’t work the crazy hours I worked when I was 18. My average weekly hours dropped to more like 50. All-nighters became pretty rare—but, as we shall see, not entirely absent.

As I matured, I realized that my worst technical mistakes were made during those periods of frenetic late-night energy. I realized that those mistakes were huge impediments that I had to constantly work around during my truly wakeful hours.

Then came the event that made me reconsider my ways. My future business partner, Jim Newkirk, and I were pulling an all-nighter. Sometime around 2 a.m., we were trying to figure out how to get a piece of data from a low-level part of our system to another part that was much higher up the execution chain. Returning this data up the stack was not an option.

We had built a “mail” transport system within our product. We used it to send information *between* processes. We suddenly realized, at 2 a.m., with caffeine roaring through our veins and all our faculties operating at peak efficiency, that we could have the low-level part of the process mail that piece of data to itself where the high-level part could fetch it.

Even today, more than three decades later, whenever Jim and I want to describe someone else’s unfortunate decision, we say: “Uh-oh. They just mailed it to themselves.”

I won’t bore you with all the horrible, nitty-gritty details about why that decision was so awful. Suffice it to say, it cost us many times the effort that we thought we were saving. And of course, the solution became too entrenched to reverse, so we were stuck with it.⁵

5. This was a decade before I would learn about TDD. Had Jim and I been practicing TDD back then, we could have easily backed out of that change.

## MARATHON

That was the moment that I learned that a software project is a marathon, not a sprint, nor a sequence of sprints. In order to win, you must pace yourself. If you leap out of the blocks and run at full speed, you’ll run out of energy long before you cross the finish line.

Thus, you must run at a pace that you can sustain over the long haul. You must run at a *Sustainable Pace*. If you try to run faster than the pace you can sustain, you will have to slow down and rest before you reach the finish line, and your average speed will be slower than the Sustainable Pace. When you are close to the finish line, if you have a bit of spare energy, you can sprint. But you must not sprint before that.

Managers may ask you to run faster than you should. You must not comply. It is your job to husband your resources to ensure that you endure to the end.

## DEDICATION

Working overtime is not a way to show your dedication to your employer. What it shows is that you are a bad planner, that you agree to deadlines to which you shouldn’t agree, that you make promises you shouldn’t make, that you are a manipulable laborer and not a professional.

This is not to say that all overtime is bad, nor that you should never work overtime. There are extenuating circumstances for which the only option is to work overtime. But they should be extremely rare. And you must be very *aware* that the cost of that overtime will likely be greater than the time you save on the schedule.

That all-nighter that I pulled with Jim all those decades ago was not the last all-nighter I was to pull—it was the second to last. The last all-nighter I pulled was one of those extenuating circumstances over which I had no control.
