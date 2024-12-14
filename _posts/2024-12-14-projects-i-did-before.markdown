---
layout: single
title:  "Projects I did before"
date:   2024-12-14 19:00:00 +0100
categories: update
---

It will take me a while to write about my previous projects. In meanwhile, a list with a few major projects summary will have to do. It goes from the newest to oldest.

- Developed as a part of a team a complex program generating interactive Business reports for over 20 clients each with multiple e-shops. The program is written in `Python`, versioned at `GitHub`, `Dagster` is used for orchestration tool. It uses `Google Cloud` for storage and `BigQuery` data warehouse. It pulls data from client feeds and GA4, generating BigQuery tables, which are connected to `Looker Studio` reports. I upgraded `Greykite forecasting library` to newer Python and used it to produce forecasts of interesting metrics too, customizing the models in `Jupyter notebooks`.

- Created and for 4 years developed and maintained a program for generating interactive Business reports for over 20 clients each with multiple e-shops. The program is written in `Python`, versioned at `GitHub`, ran on the company's linux server. It uses `BigQuery` data warehouse. It pulls data from client feeds and Universal Analytics, generating BigQuery tables, which are connected to `Looker Studio` reports. 

- Integrated stellar catalog GAIA DR2 (580 GB compressed) and GAIA DR3 (10TB) into an observatorys astrometric workflow. Due to the catalogs sheer size, `MariaDB` database with Spatial index turned out to be the fastest solution - at the observatory's hardware, it takes about 2 seconds to find and load the several thousand stars in the field of view of the telescope.

- Created custom control software in `Python` for scientific cameras (CCD, CMOS). It is a custom software for an observatory, containing all the usual functions, integrated control of the telescope's accessories (cooling, shutter, focuser..) and tied into automatically triggering star identification.
     
- Designed algorithms for telescope data transformation and analysis, resulting in successful observations of the only two known interstellar asteroids.

  > Published in Doctoral Thesis: Numerical Methods of Image Analysis in Astrometry.	 
	 
- Created an astrometric precovery program to comb extensive archive of the observatory's images for possible precovery images of newly discovered trans-neptunian objects, which led to significant refinement of orbit of dwarf planet MakeMake. 

  > Published in: Asteroids, Comets, Meteors 2008: TNO Precovery Survey Using the KLENOT Telescope Archive.   	 
	 
- Continually developed and refashioned old tools of the observatory written in `Object Pascal`, introduced `MySQL` and maintained databases in `MySQL`, `MariaDB`, rewrote old c++ scripts ran in linux into `Python`.  
