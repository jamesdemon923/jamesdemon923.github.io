---
layout: post
title: Optical flow
date: 2023-06-14
description: About the optical flow and related algorithms
tags: Report
categories: Vision
giscus_comments: true
related_posts: true
toc:
  sidebar: left
---
## Optical flow

Optical flow is the pattern of apparent motion of image objects between two consecutive frames caused by the movement of object or camera. It is 2D vector field where each vector is a displacement vector showing the movement of points from first frame to second. Consider the image below.

<img src="assets/img/optical_flow/optical_flow_basic.jpg" width="100" height="100" align="center" />

It shows a ball moving in 5 consecutive frames. The arrow shows its displacement vector.

Optical flow works on several assumptions:

1. The pixel intensities of an object do not change between consecutive frames.

2. Neighboring pixels have similar motion.

Consider a pixel $$I(x,y,t)$$ in first frame (A new dimension, time, is added here). It moves by distance $$(dx,dy)$$ in next frame taken after $$dt$$ time. Since those pixels are the same and intensity does not change:


$$
I(x,y,t)=I(x+dx,y+dy,t+dt)
$$


Then take taylor series approximation of right-hand side, remove common terms and divide by $$dt$$ to get the following equation:


$$
f_{x}u+f_{y}v+f_{t}=0
$$


where:


$$
f_{x}=\cfrac{∂f}{∂x};f_{y}=\cfrac{∂f}{∂y}\\\
u=\cfrac{dx}{dt};v=\cfrac{dy}{dt}
$$


Above equation is called **Optical Flow equation**. In it, we can find $$f_{x}$$ and $$f_{y}$$, they are image gradients. Similarly ft is the gradient along time. But (u,v) is unknown. We cannot solve this one equation with two unknown variables. So several methods are provided to solve this problem and one of them is Lucas-Kanade.

## Algorithms

### Traditional algorithms

The ideal output of an optical flow algorithm is an estimated correlation of the velocity of each pixel in two frames, or equivalently, a vector of displacements for each pixel in one image, indicating the relative position of that pixel in the other image, which is often called "dense optical flow" if every pixel in the image is used.

There is also an algorithm called "sparse optical flow" that tracks only a subset of points in the image. This algorithm is usually fast and reliable because it focuses attention only on specific points that can be easily tracked, and the computational cost of sparse tracking is much lower than that of dense tracking.

#### [Lucas-Kanade Optical flow (sparse optical flow)](https://dl.acm.org/doi/10.5555/1623264.1623280)

#### Horn-Schunck Optical flow (dense optical flow)

### Deep learning algorithms

#### [FlowNet](https://arxiv.org/pdf/1504.06852.pdf)

<img src="assets/img/optical_flow/Structure of FlowNet.png" width="100" height="100" align="center" />

#### [FlowNet 2.0](https://arxiv.org/pdf/1612.01925.pdf)

<img src="assets/img/optical_flow/Structure of FlowNet2.png" width="100" height="100" align="center" />

#### [PWC-Net](https://arxiv.org/pdf/1709.02371.pdf)

Refer to Figure,3

#### [MaskFlownet](https://arxiv.org/pdf/2003.10955.pdf)

Maskflownest takes the effect of occlusion into account when solving for the optical flow field

#### [PPAC-HD3](https://arxiv.org/pdf/2003.14407.pdf)
