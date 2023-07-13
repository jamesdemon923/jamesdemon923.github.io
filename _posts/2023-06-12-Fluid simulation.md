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

## Representation

### Particle

Use [Smoothed Particle Hydrodynamic (SPH)](https://en.wikipedia.org/wiki/Smoothed-particle_hydrodynamics)

For example, a glass of water, [using SPH directly with particles to simulate](http://mmacklin.com/pbf_sig_preprint.pdf), no grid required.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fluid_simulation/SPH for small water.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

### Grid

Solve [Navier Stokes Equations (NS equation)](https://en.wikipedia.org/wiki/Navier%E2%80%93Stokes_equations)

A small lake is simulated on a certain coarse **grid** using the Navier-Stokes equation (NS equation) or the Euler equation. And it can extend to the [3D smoke simulation](http://web.stanford.edu/class/cs237d/smoke.pdf).

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fluid_simulation/smoke simulation.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

## Other approaches to simulate

1. Use [FFT](http://www-evasion.imag.fr/Membres/Fabrice.Neyret/NaturalScenes/fluids/water/waves/fluids/waves/Jonathan/articlesCG/simulating-ocean-water-01.pdf) to simulate the ocean.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fluid_simulation/FFT.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
2. Use [wave curves](https://visualcomputing.ist.ac.at/publications/2020/WaveCurves/) to simulate the Lagrangian water waves

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fluid_simulation/wave curves.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
