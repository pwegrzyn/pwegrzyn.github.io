---
authors:
- name: "Patryk Węgrzyn"
date: 2021-08-27
linktitle: The ETC Principle
type:
- post 
- posts
title: The ETC Principle
weight: 1
categories:
- software
---

There's quite a few popular software engineering principles (often remembered in the form of catchy acronyms):
* S.O.L.I.D.
  * **S**ingle responsibility: A component should have a single reason to change. 
  * **O**pen-closed: A component should be easily extendable without much need for modification. 
  * **L**iskov substitution: A derived class should be easily swappable with it's base class. 
  * **I**nterface segregation: Write concise interface definitions with a single purpose. 
  * **D**ependency inversion: High-level components should not depend on low-level components, low-level components should instead depend on interfaces defined by high-level components.
* DRY - Don't repeat yourself: A unit of knowlegde should have only one, precise, unambiguous definition in the system.
* KISS - Keep it simple, stupid: Don't try to be smart, just for the sake of it. Simple code is better code.
* YAGNI - You ain't gonna need it: Don't try to add unnecesarily complex structures and patterns to your code just to make it maximally generic and abstract - you probably will get away with a simpler and more concrete solution.
* TDA - Tell, don't ask: A function should instruct objects to perform certain actions, instead of asking them for details and doing it itself.
* SAP - Stable Abstractions Principle: The more abstract a component is, the more stable it should be, and vice versa.
* LC/HC - Low coupling, high cohesion: Isolate logically seperate components from each other.
  
... and many others. In fact, there's so many of them, that an unexperienced programming adept could feel overwhelmed by the sheer number of rules her code should adhere to. Instead of being a help, it can actually hamper your productivity, since the subtle act of balancing these principles can be highly non-trivial in practical settings. For example, replication of logic clearly is bad, however extraction of common subcomponents can lead to increased coupling. Also, presumably you don't want to write super-generic code with tons of abstractions, since that'll make it harder to understand, but at the same time, you want it to be maximally extendable in the future. The process of creating high-quality software lies somewhere in a wide spectrum spanned by all these rules.

However, despite this richness of principles, I think there's a single, most fundamental rule of software engineering, from which all other can be derived:

### **ETC** - Whatever design or implementation decision you make, ensure that it makes your code **E**asier **T**o **C**hange in the future

When writing each line of code, subconsciously ask yourself, if this code will be easy to change in a few months, whenever the answer even remotely sounds like "no", then you can probably do better. Think how you can improve:
* readability,
* comprehensibility,
* testability,
* extendability.

The essence of **ETC** is even present in the name of our industry - **soft**ware engineering. As programmers, we should strive to be experts in producing **soft** solutions to *hard* problems :)

For anyone interested in learning more about designing and implementing elastic software projects I recommend Uncle Bob's ["Clean Architecture"](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164) which focuses on the more technical side and [Domain-Driven Design](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215) by Eric Evans which is more about modelling.