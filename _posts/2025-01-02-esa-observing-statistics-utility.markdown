---
layout: single
title:  "ESA Observing Statistics Utility"
date:   2025-01-02 19:00:00 +0100
categories: projects
tags: astrophysics, xml, python, esa, poetry, github
---

I wrote a small utility to produce statistics from ADES astrometric observations. 

## Assignment 

The Klet observatory is part of European Space Agency's CARMEN sensor network for asteroids. It provides ESA with observations 
in requested format, various statistics and reports at project meetings. As per one of ESA's requirements, 
when reporting the observations on the monthly report, ESA wants to be provided the following information:

> Include a table in the report with the name (provisional and/or designated) of the targets, the V mag and the time 
> on sky (number of images times the exposure time) and a flag for being or not reported to the MPC.

To generate the statistic, I wrote a small program `esa-obs-stats` in Python, using `Poetry` for package management. 

## Input

The input comes as `.xml` files in `/obs-data/`.  
The files contain astrometric observations in [ADES format](https://minorplanetcenter.net/iau/info/ADES.html),
as they are sent from the observatory to the Minor Planet Center. 

[The Minor Planet Center](https://minorplanetcenter.net/) is a single worldwide location 
for receipt and distribution of positional measurements of minor planets, comets and moons. 
It operates under the auspices of Division F of the International Astronomical Union,
and is funded from a NASA Near-Earth Object Observations program grant. 

Only part of the observation file is used to produce the statistic.  
Here is a minimal working example:

```xml
<ades version="2017">
  <obsBlock>
	<obsData>
      <optical>
        <trkSub>A11gr7L</trkSub>
        <obsTime>2024-12-26T17:27:59.727Z</obsTime>
        <mag>17.3</mag>
        <exp>3</exp>
      </optical>
    </obsData>
  </obsBlock>
</ades>
```

## Output

The produced statistics is saved as `result.txt` file. Originally, I made it a `.csv` file, 
but was asked for text form of the output. The final output looks like this:  

```
TARGET         V mag  Time on sky Reported to the MPC?
=======================================================                  
2012 AD3       19.7   100.0       Y                                     
2016 JW5       19.5   80.0        Y                   
2016 VR5       16.7   80.0        Y 
```

## Repository 

The program's [GitHub repository can be found here.](https://github.com/Shavril/esa-obs-stats/)
