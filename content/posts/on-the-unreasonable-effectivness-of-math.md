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

In his famous 1960 article Eugene Wigner argued about "the unreasonable effectiveness of mathematics in the natural sciences". The main point made here was the existance of a seemingly unexpected natural relationship between math and physics. Specifically, why does math lend itself so well to modelling of physical reality? Why are physical laws and processess even expressable as mathematical equations in the first place? Where does this correspondence between abstract platonic ideas and concrete physical observations originate from?

My take on this is as follows.

In essence, computer science (or computation and algorithms in general) provides the underlaying link to bridge these two - math and physics are two ways of looking at the same, more general concept. Let's look at both from this computational perspective.

Math is all about taking some initial set of "self-evident truths" and constructing from them other more advanced (and less self-evident) "truths". These proofs are essentially computer programs where the input data are the initial axioms and the rules of transformation are the rules of logical reasoning. In contrast to typical computer programming, in math we don't create proofs (i.e. "programs") to be able to run them quickly to find out the outputs for various inputs, rather we construct them to discover how the abstract property of "truthness" is propagated from basic observations (inputs) to more abstract and sophisticated observational constructs. The exact definition "truthness" might not even be that important, but let's assume we call something "true" when it corresponds to some possible physical state which makes sense in the given context.

Physics, when viewed from a computational viewpoint, has a strikingly similar nature. A physical process is, in essesnse, a computer program. The inputs to this program are the initial state of the universe at a given point in time, and the rules of transformation are the laws of physics (whatever they might be). As time passes, the universe proceeds with this computation to generate a new updated output states.

In computer science (or in programming in general), we can be presented with any possible input data whatsoever, we are not bound to only some fixed set of input states as in physics (where the big bang essentially provided the main input state) or in math (where the input states are some subsets of self-evident truths, which correspond to different axiom systems). In fact, in programming we also have arbitrary rules (in math and physics these are also fixed and provided ad-hoc), so, when writing computer programs, we're actually interested in running the specified computations on the specified input data as quickly as possible, to discover what will be the output for a given input. This also shows why computer science is, in some sense, more abstract and powerful than math and physics (operating on arbitrary inputs and with arbitrary rules).

All this is possible thanks to the universality of computation - even simple rules give rise to arbitrarily complicated processes and outputs. This universality is essentially why math, physics and programming are simply aspects of the same underlaying phenomenon, just viewed from different historical perspectives.