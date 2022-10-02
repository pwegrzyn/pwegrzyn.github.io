---
authors:
- name: "Patryk Węgrzyn"
date: 2022-10-02
linktitle: On the (Un)reasonable Effectivness of Math in Physics
type:
- post 
- posts
title: On the (Un)reasonable Effectivness of Math in Physics
weight: 1
categories:
- math
---

In [his famous 1960 article](https://en.wikipedia.org/wiki/The_Unreasonable_Effectiveness_of_Mathematics_in_the_Natural_Sciences) Eugene Wigner argued about "the unreasonable effectiveness of mathematics in the natural sciences". The main point made here was the existance of a seemingly unexpected natural relationship between math and physics. Specifically, why does math lend itself so well to modelling of physical reality? Why are physical laws and processess even expressable as mathematical equations in the first place? Where does this correspondence between abstract platonic ideas and concrete physical observations originate from?

My take on this is as follows.

In essence, computer science (or computation and algorithms in general) provides the underlaying link to bridge these two - math and physics are two ways of looking at the same, more general concept. Let's look at both from this computational perspective.

Math is all about taking some initial set of "self-evident truths" and constructing from them other more advanced (and less self-evident) "truths". These proofs [are essentially computer programs](https://en.wikipedia.org/wiki/Curry%E2%80%93Howard_correspondence) where the input data are the initial axioms and the rules of transformation are the rules of logical reasoning. Interestingly, in contrast to typical computer programming, in math we don't create proofs (i.e. "programs") to be able to run them quickly to find out what will be the outputs for various inputs (inputs are pretty much always the same and immutable), rather we construct them to discover how the abstract property of "truthness" is propagated from fixed basic observations (inputs) to more abstract and sophisticated observational constructs. The exact definition "truthness" might not even be that important, but a nice perspective is to assume we call something "true" when it corresponds to some plausible physical state which makes "physical" sense in the given context.

Physics, when viewed from a computational viewpoint, has a strikingly similar nature. A physical process is, in essesnse, a computer program. The inputs to this program are the initial state of the universe at a given point in time, and the rules of transformation are the laws of physics (whatever they might be - Newton's laws of motion, special relativity, QED, string theory). As time passes, the universe proceeds with this computation to generate new updated output states. So, same as with maths, we have a fixed input domain, a fixed set of transformation rules, and both these two are combined to progressively generate new output states indefinitely. These outputs are: "not self-evident truths" in the case of math, and physical states (i.e. slices of the spacetime manifold) in case of physics.

In fact, in computer science (or in programming and algorithms in general), we can be presented with ANY possible input data whatsoever, we are not bound to only some fixed set of input states as in physics (where the big bang essentially provided THE main input state) or in math (where the input states are some subsets of "self-evident truths", which correspond to different axiom systems, e.g. [ZFC](https://en.wikipedia.org/wiki/Zermelo%E2%80%93Fraenkel_set_theory)). In fact, in programming we also have arbitrary rules (in math and physics these are also fixed and provided ad-hoc by the universe). So, when writing computer programs, we're actually interested in running the specified computations on the specified input data as quickly as possible, as efficiently as possible, and as often as possible, to discover what will be the output for a given input. This also shows why computer science is, in some sense, more abstract and powerful than math and physics - it allows to operate universally on arbitrary inputs.

All this is possible thanks to the [universality of computation](https://en.wikipedia.org/wiki/Universal_Turing_machine) - even simple rules give rise to arbitrarily complicated processes and outputs. This universality is essentially why math, physics and programming are simply aspects of the same general underlaying computational phenomenon, just viewed from different historical perspectives.