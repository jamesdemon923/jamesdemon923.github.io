---
layout: post
title: Fluid Simulation
date: 2023-06-12 10:14:00-0400
description: Introduction to Fluid Simulation
tags: Report
categories: Graphics Simulation
giscus_comments: true
related_posts: true
toc:
  sidebar: left
---
## Introduction

For fluid simulation, the first step is to confirm the scale, because for different scales, we have different approaches. And, "realism" and "controllability" are very important. For realism, we need to solve the differential equations, while for controllability, we sometimes have to adjust the dependence on the numerical solution of the equations

## Fluid simulation at different scales
### Small

For example, a glass of water, [using SPH or directly with particles to simulate](http://mmacklin.com/pbf_sig_preprint.pdf), no mesh required.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fluid_simulation/SPH for small water.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

### Median

A small lake is solved on a certain coarse grid using the Navier-Stokes equation (NS equation) or the Euler equation. And it can extend to the [3D smoke simulation](http://web.stanford.edu/class/cs237d/smoke.pdf).

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fluid_simulation/smoke simulation.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

### Large

Use [FFT](http://www-evasion.imag.fr/Membres/Fabrice.Neyret/NaturalScenes/fluids/water/waves/fluids/waves/Jonathan/articlesCG/simulating-ocean-water-01.pdf) to simulate the ocean.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fluid_simulation/FFT.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

