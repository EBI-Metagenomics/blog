---
published: true
category: tools
emg:
  text: Metagenomics Toolkit
  url: >-
    https://github.com/EBI-metagenomics/emg-toolkit
layout: post
---
![Python script]({{site.baseurl}}/assets/media/images/posts/ico_code_EMG_grey.png)
Need to compile metadata to perform trait associations using our metagenomic data? Interested in correlating species abundance with the origin of the sample to identify organisms associated with a particular environment or state? Try our latest metagenomics toolkit (called: “mg-toolkit”) - a beta version of a tool to enable scientists to download all of the sample metadata for a given study to a single csv file. Simply install as follows:

    $ pip install --update mg-toolkit
    $ mg-toolkit original_metadata -a ERP001736 

or use it directly from within your Python script:

    >>> from mg_toolkit.metadata import OriginalMetadata
    >>> om = OriginalMetadata("SRP034967")
    >>> om.save_to_csv(om.fetch_metadata(), "SRP034967_metadata.csv")

We will add more useful tools to help processing metadata and annotations in the future. 

Metadata matters!
