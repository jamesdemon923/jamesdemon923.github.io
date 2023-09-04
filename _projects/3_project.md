---
layout: page
title: Denoise in RTRT
description: Denoise in real-time ray tracing
img: assets/img/denoise_in_RTRT/cover.jpg
importance: 1
category: Fun

---

## Setup

**Operating & compiling environment**:

* Visual studio 2022 (Windows 11)

**Scripts:**

* Use **build.bat**/**build.sh** to build the project
* **image2video** used to transfer the output from pictures to videos (Need [ffmpeg](https://ffmpeg.org/))

## Code

**[Github repository](https://github.com/jamesdemon923/Denoise_in_RTRT)**

## Joint Bilateral Filter

For denoising, we can filter out the noisy signal by various filters. 

The simplest one is **Gaussian filter**. For the final color of a target pixel, Gaussian filter will consider the color contribution from all adjacent pixels, and the weight of the contribution decreases with increasing distance from the target pixel, which ultimately achieves the purpose of removing the high frequency signal. However, this kind of filtering will also <u>blur the boundary of the object</u>, and we usually want to remove only the noise and maintain the object boundary sharp.

**Bilateral filter** is a good solution for this problem. Since there are often drastic changes about color in two sides of the object boundary, the bilateral filter takes into account the difference (distance) between colors, i.e., if the larger the difference between the color of the two pixels, the smaller the contribution in order to retain the edge information. 

**Joint bilateral filter**, on the other hand, takes into account more reference information, such as depth, normal, and world coordinates to better guide the filtering operation.

In the following picture, **A and B need considering depth; B and C need considering normal; D and E need considering color.**

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/denoise_in_RTRT/Theory/Joint Bilateral Filtering.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

### Filter kernel:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/denoise_in_RTRT/Equation/Filter Kernel.png" class="rounded" zoomable=true %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/denoise_in_RTRT/Equation/Dnormal.png" class="rounded" zoomable=true %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/denoise_in_RTRT/Equation/Dplane.png" class="rounded" zoomable=true %}
    </div>
</div>

In the above equations, $$\widetilde{C}$$ is the noisy input image, $$D_{normal}$$ is the angle between the normals of two points (**for normal information**), $$D_{plane}$$ provides a better metric than just simply calculating the difference between two depths (**for depth information**).

### Temporal Accumulation:

#### Motion vector

The projection equation:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/denoise_in_RTRT/Equation/Projection.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
This is the advantage of graphics: **mastering the matrices of the entire pipeline for calculating conveniently.**

#### Accumulation:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/denoise_in_RTRT/Equation/Temporal accumulation.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>


For clamping, it is first necessary to compute the mean $$\mu$$ and variance $$\sigma$$ of $$\bar{C}^{(i)}$$ in a 7x7 neighborhood, and then to clamp the color of the previous frame $$C^{i-1}$$ into the range $$(\mu-k\sigma,\mu+k\sigma)$$.

### A-Trous wavelet:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/denoise_in_RTRT/Theory/A-Trous Wavelet.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

## Pipeline

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/denoise_in_RTRT/Theory/pipeline.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

## Result

<table>
    <tr>
        <th colspan="1">Before denoise</th>
        <th colspan="1">After denoise</th>
    </tr>
    <tr>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/Before denoise.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}</center></td>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/After denoise.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}</center></td>
    </tr>

<table>
    <tr>
        <th colspan="2">Result of cornell box</th>
    </tr>
    <tr>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/box-input.gif" class="img-fluid rounded z-depth-1" zoomable=true caption="Input" %}</center></td>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/box-After denoise.gif" class="img-fluid rounded z-depth-1" zoomable=true caption="After denoise for per frame" %}</center></td>
    <tr>
    <tr>	
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/box-After TemAccumulation.gif" class="img-fluid rounded z-depth-1" zoomable=true caption="After temporal accumulation" %}</center></td>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/box-with A-Trous.gif" class="img-fluid rounded z-depth-1" zoomable=true caption="Accelerated by A-Trous" %}</center></td>
    </tr>
<table>
    <tr>
        <th colspan="2">Result of pink house</th>
    </tr>
    <tr>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/pinkroom-input.gif" class="img-fluid rounded z-depth-1" zoomable=true caption="Input" %}</center></td>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/pinkroom-Only TemAccumulation without filter.gif" class="img-fluid rounded z-depth-1" zoomable=true caption="Only temporal accumulation without filter" %}</center></td>
    <tr>
    <tr>	
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/pinkroom-After TemAccumulation.gif" class="img-fluid rounded z-depth-1" zoomable=true caption="After temporal accumulation" %}</center></td>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/pinkroom-with A-Trous.gif" class="img-fluid rounded z-depth-1" zoomable=true caption="Accelerated by A-Trous" %}</center></td>
    </tr>

<table>
    <tr>
        <th colspan="1">Cost of time</th>
    </tr>
    <tr>
        <td ><center>{% include figure.html path="assets/img/denoise_in_RTRT/Result/Time.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}</center></td>
    </tr>

