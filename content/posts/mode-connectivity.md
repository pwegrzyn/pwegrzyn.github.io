---
authors:
- name: "Patryk Węgrzyn"
date: 2021-08-15
linktitle: Mode connectivity
type:
- post 
- posts
title: Loss landscapes, mode connectivity and generalization of deep neural nets
weight: 1
categories:
- ml
- software
---

Deep learning's impact on the fields of computer science, artificial intelligence and many others cannot be understated. Some even go as far as to say that this type of automated reasoning based on data and not on explicit rules will spark a new era of software [[1]](#1). However, despite the tremendous success of deep neural nets, their remarkablew effectivness and good generalization capabilites are not yet fully understood. Over the last couple of months I decided to dig a bit deeper into the fundamental aspects of deep learning such as network architecture, depth, width, optimizer method, loss surface and others, to try to develop an intuition on what makes some models great and others mediocre. I present my key observations in this article.

Loss landscape visualization
--------


Structural symmetries
--------
For many years it has been speculated that the inherent symmetries in network architectures should give rise to many semi-equivalent minima in the loss function. The reasoning behind this conjecure goes something like this: picture two neurons within a single layer in a deep network. These neurons have some impact on the final ouput of the network. Now try a different permutation of them, i.e. swap their weights. Clearly the output of the network should remain the same, even though we changed the model structure. This means that these two permutations should correspond to two minima in the loss function which are closely related to each other. What do we mean by *related*? Imagine that instead of a discrete swap, we change the neurons' weights continuously: we gradually decrease weights of one neuron and increase the weights of the other one. At some point during this process, the weights will have the same value. Finally, we continue the process untill the weights have their values fully swapped. How would this transformation affect the loss surface? It turns out that, staring from a given minimum, the continuous swap would take us through a low loss *valley*. Somewhere in the middle of the valley, directly in the point corresponding to the neurons having equal weights, we encounter a saddle point, and then finally, continuing along the valley, we reach its end - a second minimum representing the neuron weights being fully swapped [[2]](#2). THis leads us straight to the next point - mode connectivity.

Mode connectivity
--------


## References
<a id="1">[1]</a>
Andrej Karpathy (2017)
*Software 2.0.*
[https://karpathy.medium.com/software-2-0-a64152b37c35](https://karpathy.medium.com/software-2-0-a64152b37c35)

<a id="2">[2]</a>
Johanni Brea, Berfin Simsek, Bernd Illing, Wulfram Gerstner (2019)
*Weight-space symmetry in deep networks gives rise to permutation saddles, connected by equal-loss valleys across the loss landscape.*
https://arxiv.org/abs/1907.02911