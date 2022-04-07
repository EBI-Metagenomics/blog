---
published: true
category: tools
title: MGnify’s Notebook Server with MGnifyR launched
emg:
  text: Open Notebooks
  url: >-
    https://notebooks.mgnify.org
layout: post
---
![Illustration of a catalogue with a taxonomic tree]({{site.baseurl}}/assets/media/images/posts/notebook_server/notebooks-banner.png){:width="136px"} 
We are excited to announce the launch of [MGnify’s Notebook Server](http://notebooks.mgnify.org). It provides an online, no-installation-needed, [Jupyter Lab](https://jupyter.org) environment for users to explore programmatic access to MGnify’s datasets using [Python](https://www.python.org) or with [R](https://www.r-project.org/about.html) using the [MGnifyR](https://github.com/beadyallen/MGnifyR) package.

<iframe width="560" height="315" src="https://www.youtube.com/embed/B8rw7GTX9GQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### Watch our [video tutorial on YouTube](https://www.youtube.com/watch?v=B8rw7GTX9GQ).

The quantity and richness of [metagenomics-derived data in MGnify](https://www.ebi.ac.uk/metagenomics/search) grows every day. The [MGnify website](https://www.ebi.ac.uk/metagenomics/) is the best place to start exploring and searching the MGnify database, and allows users to download modest query results as CSV tables.

For larger queries, or more complex requirements like fetching metadata from samples across multiple studies, a programmatic access approach is far better.

![10 popular biomes and the number of database entries for them]({{site.baseurl}}/assets/media/images/posts/notebook_server/selected-biomes.png){:width="100%"} 
_MGnify database entries for selected biomes_

Programmatic access – fetching data from MGnify using a terminal command or code script – uses the [MGnify API](https://docs.mgnify.org/en/latest/api.html) ([Application Programming Interface](https://en.wikipedia.org/wiki/API)). The API provides access to every data type in MGnify: [Studies](https://www.ebi.ac.uk/metagenomics/api/v1/studies), [Samples](https://www.ebi.ac.uk/metagenomics/api/v1/samples), [Analyses](https://www.ebi.ac.uk/metagenomics/api/v1/analyses), [Annotations](https://www.ebi.ac.uk/metagenomics/api/v1/annotations/interpro-identifiers), [MAGs](https://www.ebi.ac.uk/metagenomics/api/v1/genome-catalogues) etc: it is what lies behind the MGnify website. Using the API means you can fetch more data than is possible via the website, and can help you write reproducible analysis scripts.

The API can be explored interactively online, using the [API Browser](https://www.ebi.ac.uk/metagenomics/api/v1/). But actually **using** the API first requires knowledge and/or installation of tools on your computer. This might range from a command line tool like [cURL](https://curl.se), to learning R and setting up the [R Studio](https://www.rstudio.com) application, to setting up a [Python](https://www.python.org) environment and installing a suite of [packages used for data analysis](https://pandas.pydata.org). Second, the API returns most data in [JSON format](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON): this is standard on the web, but less familiar for bioinformaticians used to TSVs and dataframes.

The [MGnify Notebook Server](http://notebooks.mgnify.org) and [MGnifyR package](https://github.com/beadyallen/MGnifyR) are designed to bridge these gaps. Users can launch an online R and Python coding environment in their browser, without installing anything. The environment is hosted by EMBL’s [Cell Biology and Biophysics Computational Support team](https://www.embl.org/research/units/cell-biology-biophysics/cbbcs/), who support computational projects across EMBL. It already includes the main libraries needed for communicating with the MGnify API, analysing data, and making plots. It uses the popular [Jupyter Lab](https://jupyter.org/) software, which means you can code inside [Notebooks](https://jupyter-notebook.readthedocs.io/en/latest/): interactive code documents.

There are example Notebooks written in both R and Python, so users can pick whichever they’re more familiar with. 

For many users, the online environment can serve as an extension of the website: enabling them to call a few queries on the API, join some data together, and create a datafile or plot they can save to their own computer. The MGnify website has deep-links into the Notebook Server that let users jump from looking at a Study on the website, for example, into a pre-configured R Notebook ready to access that Study using the API.


![The Programmatic Access section of a Sample page on the MGnify website]({{site.baseurl}}/assets/media/images/posts/notebook_server/programmatic-access.png){:width="100%"} 
_(This feature is available on the [MGnify Beta website](https://www.ebi.ac.uk/metagenomics/beta/).)_

For more advanced use cases, the Notebooks serve as an introduction to using the API, and guide users on [how to set up a local environment to use the API](https://github.com/ebi-Metagenomics/notebooks/#embl-ebi-mgnify-example-notebooks).

## MGnifyR
The MGnify Notebook Server also provides access and examples for the [MGnifyR](https://github.com/beadyallen/MGnifyR) package, created by Ben Allen. MGnifyR wraps the MGnify API in R functions that will feel more familiar to R users and translates data from the API’s JSON standard format into [dataframes](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/data.frame) and [Phyloseq](https://joey711.github.io/phyloseq/) objects. It also provides features for cross-study analysis workflows, like computing differential abundance.
