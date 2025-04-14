---
layout: single
title:  "Simple Sales Report in Looker Studio"
date:   2025-04-14 10:00:00 +0100
categories: projects
tags: looker_studio bigquery csv kaggle
---

A small example report in Looker Studio.

## Input Data 

I used [this simple dataset from Kaggle](https://www.kaggle.com/datasets/ihelon/coffee-sales/data) for this example dashboard.

In BigQuery, I created a new dataset in the web interface, and inside it a new table - for the Source, I set `Create table from upload`, and set the `index_1.csv` file I downloaded from Kaggle. I also ticked `Autodetect Schema`, and then ran the table creation. Here's an example of the first ten entries in the BigQuery table.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/simple-sales-report-in-looker-studio-01.png){: .align-center}

## Looker Studio Report

Next step is creating the Looker Studio report. First, I added the data table through Resource > Manage added data sources > ADD A DATASOURCE, then I started to work on the report itself. I created a couple of graphs, custom color scheme, computed fields, added a free use license coffee cup picture, and date control. And this is how the result looks like. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/simple-sales-report-in-looker-studio-02.png){: .align-center}

[The report in Looker Studio](https://lookerstudio.google.com/u/0/reporting/09f84ffd-5af5-409d-91a4-b124c6fcb22f/page/7srGF) is interactive. You can limit the data displayed by a date range control, read the values by hovering over the graphs, click the graphs data to limit viewed data to a certain time or coffee kind, sort the table, or change the level of detail in the graph and table using their Drill down option to switch between monthly, weekly and daily aggregation. Feel free to give it a try!

