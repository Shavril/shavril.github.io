---
layout: single
title:  "Simple Taipy Stock Dashboard"
date:   2024-12-25 19:00:00 +0100
categories: tutorials
tags: github python poetry pandas plotly scikit-learn taipy kaggle
---

Simple data science dashboard using `Taipy`. I found a good looking [Youtube Tutorial from MariyaSha](https://www.youtube.com/watch?v=hxYIpH94u20) on Taipy package in Python, and since I usually use Looker Studio for interactive dashboards, I wanted to give it a try. There were some hiccups along the way but I did it. I went with a different setup than the author, which I decribe here.

## Introduction

A stock value dashboard using `Taipy`, `Plotly`, and [a dataset from Kaggle](https://www.kaggle.com/datasets/andrewmvd/sp-500-stocks).
It will dynamically filter data, display graphs, and handle user inputs — all from scratch.

## Set up

I work on Windows 10. I use Pycharm for IDE, `Poetry` for package management, and GitHub for version control. 
I set up new repository in GitHub. In PyCharm, I created a New Project from Version control, and linked it the GitHub repository.
Opened PowerShell, went to the project's folder.

```
poetry init
```

I filled the basic info into the .toml file as instructed, and defined main dependencies interactively: 

```
taipy>=4.0.0
plotly=5.24.1
tensorflow=2.18.0
scikit-learn=1.5.2
```

Then I ran `poetry install`, and it failed to install `tensorflow-io-gcs-filesystem (0.37.1)`. It turns out the Windows build for the package is missing, `tensorflow-io-gcs-filesystem` works only up to 0.31.0 for Windows and they don’t have newer builds. I had to adjust the Python version in .toml dependencies file to `python = ">=3.10,<3.12"`, run `poetry lock` because I changed the .toml file, then

```
poetry add tensorflow-io-gcs-filesystem=0.31.0
poetry install
```

And it went through!  

In PyCharm, I added New Interpreter and navigated to `python.exe` file in the existing virtual environment Poetry created in the previous step. Time to commit into GitHub.

## First code

I inserted a basic code, 

```
import taipy as tp
import taipy.gui.builder as tgb

# create page
with tgb.Page() as page:
    tgb.text("my beautiful application goes here!")

if __name__ == "__main__":
    gui = tp.Gui(page)
    gui.run(title = "Data Science Dashboard")
```

and ran `main.py`. It serves the web application locally on [http://localhost:5000](http://localhost:5000).

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/simple-taipy-stock-dashboard-01.png){: .align-center}


## The trouble

I imported data from kaggle, added some icons and started to code along the [tutorial](https://www.youtube.com/watch?v=hxYIpH94u20). 
But, I could not import `tensorflow` package! I found [the issue here](https://github.com/python-poetry/poetry/issues/8271), it seems the package supports only `pip`, not Poetry. What worked for me was using 

```
poetry add tensorflow-intel
```

and then importing `tensorflow` package through `from tensorflow.python.keras` instead of `from tensorflow.keras`. 

But this was not the end of my woes with `tensorflow`. The package wasn't producing the computations, only an error: `module 'tensorflow.python.distribute.input_lib' has no attribute 'DistributedDatasetInterface'`. I found the error in [this issue](https://github.com/tensorflow/tensorflow/issues/61900) and solved it by using `tf-keras` instead, 

```
poetry add tf-keras
```

And changing  
```
from tensorflow.python.keras import models
from tensorflow.python.keras import layers
```
to
```
from tf_keras.models import Sequential
from tf_keras.layers import Dense
``` 

## The result

The rest of the tutorial worked like a charm. Here's my dashboard!

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/simple-taipy-stock-dashboard-02.png){: .align-center}

Seeing [the author's GitHub repository](https://github.com/MariyaSha/data_science_dashboard), she added comments and docstrings, compared to the tutorial. I also have somewhat different coding style compared to the author; I generally prefer to use f-strings, and type hints.  

Here is [my finished project on GitHub](https://github.com/Shavril/simple-taipy-dashboard).

