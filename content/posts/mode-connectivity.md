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

**Deep learning's impact on the fields of computer science, artificial intelligence and many others cannot be understated. Some even go as far as to say that this type of automated reasoning based on data and not on explicit rules will spark a new era of software [[1]](#1). However, despite the tremendous success of deep neural nets, their remarkablew effectivness and good generalization capabilites are not yet fully understood. Over the last couple of months I decided to dig a bit deeper into the fundamental aspects of deep learning such as network architecture, depth, width, optimizer method, loss surface and others, to try to develop an intuition on what makes some models great and others mediocre. I present my key observations in this article.**

Loss landscape visualization
--------
Visualizing the loss function surfaces can be a surprisingly helpful way of measuring and predicting future model performance and generalization capabilities. Unfortunately, this tasks is actually easier said than done in practice. Taking a multi-million parameter model and representing in an insightful way on a 2D/3D plot without artifacts related to dimensionality reduction is quite challanging. Some initial attempts have been proposed by Goodfellow et al. [[3]](#3). In this approach, we choose two different minima and linearly interpolate the loss surface between them, producing a 2D plot of the loss function. This methods works, but has some major issues. The biggest problem with it is that it ignores the scales of parameters on different parts of the network. A solution to this has been proposed by Li et al. [[4]](#4). Here, the authors added a normalization step: before plotting the values of the function on a parameter mesh grid, we first scale all parameters so that they absolute values have similar scales. This effectively reduces harmful artifacts in the visualization, thus producing a very robust method of investigating the geometrical structures of loss surfaces. Using this approach, the authors showed some very interesting observations: (1) very deep networks seem to have chaotic and non-convex loss landscapes; (2) the application of skip (residual) connections smooths the loss surfaces; (3) most network provably good network architectures produce highly convex loss landscapes.

Structural symmetries of neurons
--------
For many years it has been speculated that the inherent symmetries in network architectures should give rise to many semi-equivalent minima in the loss function. The reasoning behind this conjecure goes something like this: picture two neurons within a single layer in a deep network. These neurons have some impact on the final ouput of the network. Now try a different permutation of them, i.e. swap their weights. Clearly the output of the network should remain the same, even though we changed the model structure. This means that these two permutations should correspond to two minima in the loss function which are closely related to each other. What do I mean by *related*? Imagine that instead of a discrete swap, we change the neurons' weights continuously: we gradually decrease weights of one neuron and increase the weights of the other one. At some point during this process, the weights will have the same value. Finally, we continue the process untill the weights have their values fully swapped. How would this transformation affect the loss surface? It turns out that, staring from a given minimum, the continuous swap would take us through a low loss *valley*. Somewhere in the middle of the valley, directly in the point corresponding to the neurons having equal weights, we encounter a saddle point, and then finally, continuing along the valley, we reach its end - a second minimum representing the neuron weights being fully swapped [[2]](#2). THis leads us straight to the next point - mode connectivity.

Mode connectivity
--------
*Mode connectivity* refers to the observed phenomenon of different minima being connected by low loss paths. One of the first methods of finding these paths have been proposed by Garipov et al. [[5]](#5). THis is achieved by modifying the loss function to include a part maximizing a randomly sampled likelihood of a line segment connecting two minima. These can be used to find simple linear paths or more complex structures such as Bezier curves. The author's also defined an ensembling method based on this approach: we find a minimum for aboutr 80% of the computational budget, then we used a cycling cosine learning rate scheduler to move the minimum slightly along the low loss path, and we snapshot the models at certain time steps to produce the final ensemble. Following the work of Garipov, others continued to evolve the theorem of mode connectivity. Fort et al. [[6]](#6) proposed that these low loss paths are in fact parts of larger submanifolds of constant loss present in the loss landscape, suggesting that the richness of mode connectivity is much broader than first expected. Benton et al. [[7]](#7) further established that finding these manifolds is quite easy and, based on a simplex-finding algorithm, proposed a novel ensembling method which achieves SotA results. All this is to say that one should not think of the task of training deep learning models as a tedious process of finding a needle (single global minimum) in a haystack (entire parameter space), but rather as a relatively simple job of finding a *good-enough* partial minimum from a vast submanifold of low loss plateaus.

Loss geometry in the context of generalization
--------
Many studies have showed that the geometrical structures present in loss landscapes are stongly correlated with test performance and overall generalization potential. One of the main takeaways here is that wide minima are in general better than sharp minima, and that non-convex landscapes (containing many different sharp minima) are practically impossible to train. A fanstatic and intuitive explanation to this phenomenon can be seen in a recent talk by Leo Dirac (yes, he's a relative to THE Paul Dirac!) available currently on YouTube [[8]](#8). Some other great resources on this subject are these two talks by Tom Goldstein (also available on YT) [[9]](#9) [[10]](#10).

Stochastic weight averaging
--------
blah

Bonus: depth vs width
--------
blah


## References
<a id="1">[1]</a>
Andrej Karpathy (2017)
*Software 2.0.*
[https://karpathy.medium.com/software-2-0-a64152b37c35](https://karpathy.medium.com/software-2-0-a64152b37c35)

<a id="2">[2]</a>
Johanni Brea, Berfin Simsek, Bernd Illing, Wulfram Gerstner (2019)
*Weight-space symmetry in deep networks gives rise to permutation saddles, connected by equal-loss valleys across the loss landscape.*
https://arxiv.org/abs/1907.02911

<a id="3">[3]</a>
Ian J. Goodfellow, Oriol Vinyals, Andrew M. Saxe (2015)
*Qualitatively characterizing neural network optimization problems.*
https://arxiv.org/abs/1412.6544

<a id="4">[4]</a>
Hao Li, Zheng Xu, Gavin Taylor, Christoph Studer, Tom Goldstein (2018)
*Visualizing the Loss Landscape of Neural Nets.*
https://arxiv.org/abs/1712.09913

<a id="5">[5]</a>
Timur Garipov, Pavel Izmailov, Dmitrii Podoprikhin, Dmitry Vetrov, Andrew Gordon Wilson (2018)
*Loss Surfaces, Mode Connectivity, and Fast Ensembling of DNNs*
https://arxiv.org/abs/1802.10026

<a id="6">[6]</a>
Stanislav Fort, Stanislaw Jastrzebski (2019)
*Large Scale Structure of Neural Network Loss Landscapes.*
https://arxiv.org/abs/1906.04724

<a id="7">[7]</a>
Gregory W. Benton, Wesley J. Maddox, Sanae Lotfi, Andrew Gordon Wilson (2021)
*Loss Surface Simplexes for Mode Connecting Volumes and Fast Ensembling.*
https://arxiv.org/abs/2102.13042

<a id="8">[8]</a>
Leo Diract (@leopd) (2019)
*Geometric Intuition for Training Neural Networks.*
https://www.youtube.com/watch?v=Z_MA8CWKxFU

<a id="9">[9]</a>
Tom Goldstein (2018)
*What do neural loss surfaces look like?*
https://www.youtube.com/watch?v=78vq6kgsTa8

<a id="10">[10]</a>
Tom Goldstein (2020)
*An empirical look at generalization in neural nets.*
https://www.youtube.com/watch?v=kcVWAKf7UAg