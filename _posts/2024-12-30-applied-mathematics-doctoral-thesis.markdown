---
layout: single
title:  "Applied Mathematics Doctoral Thesis"
date:   2024-12-30 19:00:00 +0100
categories: projects
tags: statistics, astrophysics, image processing, python
---

Overview of my doctorate dissertation in Applied Mathematics, with pictures, results and a link to the full work.  

I was working as an astrophysicist at Klet Observatory in Czechia. The main telescope's camera had very uneven background on its pictures, which made it harder to find and measure the faint asteroids on the images. We couldn't just 'photoshop' out the background, because the images were used for scientific measurements after and that would get the results skewed. In astrophysics, an uneven background is usually solved by applying a flatfield image - an image from the camera taken without stars. Several methods to obtain it were tried and failed.  

I was convinced there must be a way to reasonably address the issue. I turned to articles, to books, and eventually to other experts - specifically, [prof. Druckműller](http://www.zam.fme.vutbr.cz/~druck/) from University of Technology in Brno, famous for [his breathtaking Solar Eclipse pictures](http://www.zam.fme.vutbr.cz/~druck/Eclipse/index.htm), which he post-processes to bring out the features in solar corona. We decided it would be a good problem to solve for a doctorate thesis and I signed up to the university with him as my thesis supervisor.  

In the thesis, titled Numerical Methods of Image Analysis in Astrometry, first I lay down an overview of astrometric process and requirements of precise astrometry, including the necessary mathematical background, steps of image pre-processing in astronomy, and outlines of use of filters. In the next part, I propose methods to level the background of images for cases when no calibration images were taken. They are based around applying filters on an image to create an artificial flatfield, which is then applied back on the image. These methods are tested on a sample of real data and the results are discussed.  

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/applied-mathematics-doctoral-thesis-01.png){: .align-center}
Left: an original image. Right: the same image processed by the SMIN algorithm described in my thesis.

While I was writing the thesis, I had a wonderful opportunity to immediately apply my new algorithms when Pan-STARRS discovered a small object with extreme speed on 19th October 2017. It was an asteroid from outside the Solar System, first of its kind ever observed, later named 1I/'Oumuamua. A metallic rock 230 per 35 meters in size hurling through the Solar System on a hyperbolic orbit, our observatory imaged it with our 1.06-m main telescope in the same night, but could not see it on the images. I treated the images with my algorithm and we were able to find and measure the interstellar asteroid. The astrometric measurements were published in [Minor Planet Electronic Circular No. 2017-U265](https://minorplanetcenter.net/mpec/K17/K17UQ5.html) together with the object's astrometry from 2.4-m telescope in New Mexico, USA, and 5.0-m telescope on Mt. Palomar, USA.  

Since then, I had fully integrated the algorithms into Klet Observatory's workflow and they came to play an essential part in obtaining high quality astrometric measurements from the telescope.  


---

HONKOVÁ, Michaela. *Numerical Methods of Image Analysis in Astrometry*. Online, Doctoral thesis, supervisor Miloslav Druckmüller. Brno: University of Technology in Brno. Faculty of mechanical engineering. Institute of Mathematics, 2018. Available at: [http://hdl.handle.net/11012/77552](http://hdl.handle.net/11012/77552). [cit. 2024-12-31].  
