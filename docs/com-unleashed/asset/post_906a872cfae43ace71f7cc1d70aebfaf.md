
## Maintainability

How effective is a software system if it cannot be upgraded or evolved over time? If there is one lesson we have learned from the Y2K problem, it is that computer programmers should be more judicious and critical of the assumptions they make about the future. Foresight and flexibility during design and implementation will be greatly rewarded. A narrow and specific solution usually must be rewritten several times as new features are requested and unexpected requirements arise.

Instead of attacking the problem in particular, strive to solve the problem in general with additional rules for the specific problem at hand. All too often we come back to old code and wish we’d put a little extra effort into decoupling a large procedure or function. It’s no fun to have to spend valuable time in a partial or complete rewrite.

With COM, this is easy to accomplish with interface inheritance. Create generic interfaces, and then implement specific behaviors to suit your problem. A great example of this technique can be seen in the IPersist family of interfaces, which are discussed in Chapter 4, “Persistent Storage.”

## Reliability

Probably the single most popular complaint about PCs is their instability. Whether it’s the fault of the operating system or third-party software, it is the user who is left with a hung program and hours of work lost.

PC versus UNIX reliability flame wars of biblical proportions have raged on Usenet for years, with no end in sight. The issue of UNIX versus PC reliability is not to be dismissed quickly, and for time-critical or life-support systems it can be a matter of life and death. Consider medical equipment with embedded software, or the navigation software on airplanes. If the patient or passenger had the option of choosing which OS they would trust their lives on, what would be the most common answer? (I would most certainly pick UNIX.)

Having worked on both platforms for almost 18 years, I have experienced the cold but faithful glow of a UNIX command prompt along with the warm, but fragile charm of a colorful PC window.

But “COM,” as Don Box once said, “is about love.” COM embraces all strangers (IUnknowns), and does not discriminate across platforms (as long as they support COM).

So we won’t discuss which operating system is more reliable, and frankly, as COM+ developers, we have little control of this part. We are normally faced with platform constraints and might not always have an option of which OS to work under.

were written in languages like C or C++ and then compiled for each desired platform. This technique didn't always work because C does not provide a standard API for rich user interfaces. To exacerbate the problem, presentation code was written along with business logic, coupling the application and producing monoliths. Porting was a whole project in its own right and required significant resources to accomplish.

Today there are browsers and platform-neutral markup languages like HTML or the new XML. It is only necessary to write the application for one platform and rely on the presentation layer to produce compatible HTML for universal compatibility.

There is one disadvantage to browsers, however. They lack rich UI controls. Technologies like Java Applets, Dynamic HTML, and ActiveX can alleviate the problem but at the cost of introducing incompatibilities among browsers.

To be truly browser-agnostic, we must do what we can with standard HTML and its primitive forms capability. In practice, this is not the sacrifice third-party ActiveX and Java component vendors would want you to believe. If buttons and text boxes are not rich enough for your application, it is possible to use image maps and offer the illusion of a sophisticated GUI.

Once again, if you haven't done so already, consider using an HTML browser as your presentation tier.

## Reusability

The most widely accepted definition of software utopia is that place where software can be built effortlessly by assembling ready-made standard components, much the way circuit boards or vehicles are manufactured today. Although we are still many decades from achieving such a grand goal, we can certainly build COM+ components today and plan to reuse them a few months from now.

The versioning properties of well-written COM+ objects guarantee that an existing interface today will continue to work (in some capacity) for the lifetime of the object. So even if new features are added to an otherwise old component, its past and present clients will not break. They just use what they need.

The COM+ specification speaks of immutable interfaces but, in reality, this turns out to be more of a suggestion. It is specified by COM+ that once a component interface is published, it should never be changed.

But it is possible to change the interface (or delete it altogether) and break the rule. This also breaks the binding contract between a COM+ object and its clients who expect to always find a specific interface. Blissfully ignorant clients of a misbehaving component will simply die after an illegal memory address rather than check to see if an interface query was successful.

COM+ does not “catch” these breaches of contract and does not warn the developer of COM+ Specification violations. That is entirely up to the developer.

Some of the tools in Visual Studio (like VB or VI) do give a warning message when deleting interfaces, but it’s still up to the developer to exercise the contract.

Without this contract, the lifetime of a component is limited and its reusability compromised.

Avoid changing interfaces after they have been published and always exercise top-down discovery (via QueryInterface) when working with other components.

## Locality

How large is the application? Does it need to be spread across machine boundaries to meet performance requirements or is one address space sufficient?

With COM’s location transparency features, it is not necessary to foresee a distributed architecture at design time to be able to use one at installation time.

With the help of MTS, components can be distributed easily across machines without either client or server knowing the difference. Only the registry knows the true location of a component and whether any proxies are used. As far as a client is concerned, a server component is living in the same address space.

## Design Tools

Many computer-aided software engineering (CASE) software tools exist to help the software architect articulate human ideas into coherent designs. One of the more popular tools for modeling architectures is Rational Rose, which is shipped with Visual Studio as Visual Modeler. Although an understanding of the unified modeling language (UML) is preferred, Visual Modeler has well-written, online documentation and tutorials to help guide UML newcomers.

Not surprisingly, the default template for building new projects in Visual Modeler is the three-tiered model (see Figure 2.8). Object-oriented fans will feel right at home with VM. Its rich feature set can overwhelm non-OO programmers, however.

![](img/112c2326f49d26b8d59aa054e14c5747_72_0.png)

**FIGURE 2.8** Visual Modeler with a default three-tiered template.

![](img/112c2326f49d26b8d59aa054e14c5747_73_0.png)

Fortunately, COM+ does not require OO skills because it is not object-oriented itself (at the binary level at least). COM is, after all, about binary interoperability.

## Beyond Object Orientation

In the last two decades, software engineering as we know it has been gradually phasing out of the procedural paradigm and into the object-oriented one. With COM/COM+, object-orientation can be taken to the next level: binary interoperability.

As a designer, this enables you to create objects that are compatible not only at a local source level, but at the application, runtime level. Being able to call on libraries or objects at runtime is not new, but doing so in an explorative way with language independence is new.

## Summary

The cost of maintaining a software system is estimated to be many times its development cost. Computer code, regardless of the language, is still a mechanized and volatile expression of human thought. We all solve problems differently, and it is reflected in the code we write. But code rots with time. It becomes obscure and unreadable. This is an inevitable fact of the software life cycle.
