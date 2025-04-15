---
layout: single
title:  "Observation Targets Graph in Tableau"
date:   2025-04-14 10:00:00 +0100
categories: projects
tags: tableau xml csv python pandas klet
---

How fast and faint objects did Klet Observatory observed lately?

## Assignment

The Klet Observatory focuses on follow-up astrometry of Near-Earth Asteroids (NEAs). Astrometry involves measuring an object's position in the sky — specifically, for asteroids, we track their location relative to the background stars. NEAs are often discovered as they make close approaches to Earth, and without precise, timely astrometric data, we wouldn’t be able to calculate their orbits accurately. As they move away from Earth and grow fainter, they can quickly become too difficult to observe, and we risk losing track of them entirely. 
That got me thinking: just how faint, and how fast, are the objects Klet Observatory typically tracks? I set out to find the answer.

## Input

I have all the information I need for this task in the observation files in `.xml`, which are sent from the observatory to [The Minor Planet Center](https://minorplanetcenter.net/). The files contain astrometric observations in [ADES format](https://minorplanetcenter.net/iau/info/ADES.html). Here's a minimal working example with two observations:

```xml
<ades version="2017">
  <obsBlock>
    <obsData>
      <optical>
        <provID>2025 FP</provID>
        <obsTime>2025-03-20T20:59:28.638Z</obsTime>
        <ra>213.011722</ra>
        <dec>37.6883271</dec>
        <mag>19.9</mag>
      </optical>
      <optical>
        <provID>2025 FP</provID>
        <obsTime>2025-03-20T20:59:43.150Z</obsTime>
        <ra>213.011555</ra>
        <dec>37.6900852</dec>
      </optical>
    </obsData>
  </obsBlock>
</ades>
```

## Preparing the data 

 The brightness of the object is denoted as `<mag>` and given in magnitudes - an astronomical logarithmic measure of brightness. The motion speed of the object is not provided directly, but we can compute it as the change in position over a given time. Motion speed in this case is typically expressed in `''/min` (arcseconds per minute). 

The positions in the sky are given in [Celestial Coordinates](https://science.nasa.gov/learn/basics-of-space-flight/chapter2-2/#hds-sidebar-nav-2) Right Ascension and Declination. In our data, Right Ascension `<ra>` is given in degrees and is the celestial spere's equivalent of longitude. Declination `<dec>`, also in degrees, is the celestial equivalent of latitude. We can calculate the positional change using the Pythagorean theorem as `sqrt(ra² + dec²)`. Technically, since the sky is a sphere, we should use a spherical triangle, but over a small area like this, the sky is nearly flat, so a planar triangle is good enough approximation.

To determine how long the positional change took, we simply compute the time difference between the two observations. Then the motion of the object in `''/min` is the positional change in arcseconds divided by the time elapsed in minutes. 

I wrote a short script in Python to load the `.xml` files from the last four months of observations into a `pandas` dataframe. Typically, during an observing night, each target is observed for some time and a set of several images is taken and measured, resulting in multiple astrometric positions for the target, before moving on to the next target. For this analysis, I grouped the observations by these sets (defined by night and target designation) and computed the motion between the first and last measurement in each set. The resulting brightness and motion data were saved into `.csv` file.

## Visualization

I loaded the file as a Data Source into Tableau Public and vizualized the data. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/observation-targets-graph-in-tableau-01.png){: .align-center}

Each circle represents a set of measurements for which the pair of brightness `Vmag` and `Motion [''/min]` was saved. The median for both axes was inserted, along with the quartiles - the light blue area around the median represents the 2nd and 3rd quartiles. Note that the motion axis is logarithmic to compress the wide range of values. The 93 sets which did not contain a brightness measurement were left out of the visualization. 

[The full size Viz](https://public.tableau.com/app/profile/michaela.honkova/viz/KletTargetMotions/Sheet1?publish=yes) is available at Tableau Public.
