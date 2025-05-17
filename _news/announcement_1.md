---
layout: post
date: 2024-05-15 15:59:00-0400
inline: false
title: New preprint - <i>Flow updates for domain decomposition of entropic optimal transport</i>
related_posts: true
tags: optimal_transport domain_decomposition
---

Domain decomposition has been shown to be a computationally efficient distributed method for solving large scale entropic optimal transport problems. However, a naive implementation of the algorithm can freeze in the limit of very fine partition cells (i.e. it asymptotically becomes stationary and does not find the global minimizer), since information can only travel slowly between cells. In practice this can be avoided by a coarse-to-fine multiscale scheme. In this article we introduce flow updates as an alternative approach. Flow updates can be interpreted as a variant of the celebrated algorithm by Angenent, Haker, and Tannenbaum, and can be combined canonically with domain decomposition. We prove convergence to the global minimizer and provide a formal discussion of its continuity limit. We give a numerical comparison with naive and multiscale domain decomposition, and show that the hybrid method does not suffer from freezing in the regime of very many cells. While the multiscale scheme is observed to be faster than the hybrid approach in general, the latter could be a viable alternative in cases where a good initial coupling is available. Our numerical experiments are based on a novel GPU implementation of domain decomposition that we describe in the appendix.

[Full preprint](https://arxiv.org/abs/2405.09400)
