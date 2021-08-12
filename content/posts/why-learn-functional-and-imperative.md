---
authors:
- name: "Patryk Węgrzyn"
date: 2021-06-24
linktitle: Functional vs imperative
type:
- post 
- posts
title: Why every developer should know both structural and functional programming
weight: 1
categories:
- software
---

The apparent feud between functional and imperative (OOP/structural) programmers have been with us since the very inception of this industry.
Usually, developers tend to identify as either a strong believer of one or the other. In my opinion, a competent programmer should be familiar with both and know when to use one over the other, based on their strenghts and weaknesses.
One is not inherently better than the other, each has characteristics making it better suited for some tasks and less optimal in others.

## Functional programming

In FP you write programs as compositions of pure functions (functions that deterministacally always produce the same output give some input). To achieve this, you must use immutable data structures. Writing in FP style also forces you to
minimize side effects, the main one being of course IO. All these aspects seem great, since they make your program easier to test and better suited for tasks which require concurrency.

However, each has it's drawback: immutability requires lots of copying or tricky algorithms to update only changing parts of data structures, managment of side effects becomes more complex and on overhead of itself and, finally, not each application can be necessarily easily and naturally written as a function composition.

In my opinion, the most practical (and beautiful) aspect of FP, comes from the [Curry–Howard correspondence](https://en.wikipedia.org/wiki/Curry%E2%80%93Howard_correspondence). Loosely speaking, this theorem states that programs are equal to mathematical proofs. This is especially prominent when your consider the most basic form of functional programming - [Lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus) (LC). In this [model of computation](https://en.wikipedia.org/wiki/Model_of_computation) you are only allowed to use 1 primitive - an abstract function object. But can you even program using ONLY functions? Yup, check [this](https://gist.github.com/pwegrzyn/31c684a7ef32a5cabb3459a9375baaeb) out.

Now consider a slightly more advanced version of Lambda calculus, with some nice syntactic sugar - Haskell.
Let's say I want to prove this mathematical theorem:
```haskell
(A -> B) -> (B -> C) -> A -> C
```
Looks easy, I know that A implies B and that B implies C, therefore A should imply C. We can translate this logical preposition to Haskell by defining a function which has a matching type signature:
```haskell
impl_comp :: (a -> b) -> (b -> c) -> a -> c
```
Now, to effectively prove this preposition, all we need to do is add a definition to this function signature:
```haskell
impl_comp = \(f::a -> b) -> \(g::b -> c) -> \(h::a) -> g (f h)
```
And, lo and behold, we have a proof for a mathematical theorem in the form of a Haskell program. Pretty cool, right? This is exactly Curry–Howard correspondence in action.

So why do I think this is the main selling point of FP? Because it clearly shows that functional programming has an inherent and close connection to logic and math in general. This in turn means that FP is perfect for use cases where the domain and business logic is complex enough to justify using more advanced abstractions and generalizations, and where you also need an almost mathematically-strict way of proving the correctness of your solutions. Compared to imperative programming, FP's lack of
mutability leads to easier work with highly concurrent systems.


## Imperative/Object-oriented/Structural programming

For most, imperative programming is a more natural way of writing code, and that shouldn't be surpring, thinking in terms of objects and steps then need to be undertaken to transform the state of these objects is closely related to how we view and interact with the world for most of the time. At the same time, we undergo many years of math education to develop a more strict way of reasoning, to deal with more complex concepts which require abstractions and generalizations. You don't calculate the Riemann metric tensor and curvature of spacetime when you want to throw a basketball. By analogy, I'd argue that you also shouldn't use advanced FP when writing simple CRUD or CLI applications.

On another note, imperative programming is much better suited as a base for considerations in the theory of computability, computational complexity and advanced algorithm development, that's because a [Turing Machine](https://en.wikipedia.org/wiki/Turing_machine), which is a mathematical model for all of them, is a sequential and imperative model by it's nature.

Finally, a sequential and imperative model of computation is much easier to implement in hardware, so when working with low-level code you are forced to use this approach. Moreover, functional programming inherently requires more memory and processing power
compared to imperative styles, so for embedded settings the latter is also a clear winner.