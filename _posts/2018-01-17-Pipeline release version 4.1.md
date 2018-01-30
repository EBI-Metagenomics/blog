---
published: true
category: spotlight
emg:
  text: Annotation Pipeline v4.1
  url: >-
    http://emg-docs.readthedocs.io/en/v4.1/analysis.html
layout: post
---
![ico_pipeline_version_newnumber_01.png]({{site.baseurl}}/assets/media/images/posts/ico_pipeline_version_newnumber_01.png)
## Analysis Pipeline v4.1 Released
As you may have seen from the EBI Metagenomics website, we have recently deployed a new version of our analysis pipeline (v4.1), which is now the default for analysis of submitted data. Our previous pipeline update (v4.0) was released approximately 6 months ago and involved substantial upgrades, including a move to a new method for identifying rRNAs and complete change to the way in which taxonomic analysis was performed. As ever, we have been busy investigating ways to improve things still further, as well as fixing some minor pipeline issues.

Over the last 6 months, there has also been a new release of the SILVA database (v132), which underpins our taxonomic analyses, as well as updates for some of the software we use for various steps in the pipeline. We have rolled all of this up into our new release, which we have been busy testing since the start of the year. We are pretty happy with the results and hope you will be too.

Changes to the pipeline include an update to SeqPrep (v1.2) and a fix to an issue we were seeing with the merging of longer paired-end reads. The new release also contains an update to the latest version of MAPseq (v1.2.2) and to the SSU and LSU taxonomic reference databases. These are now based on SILVA 132 and give improved taxonomic classification. Finally, we have fixed an issue in the RNA identification step where predicted RNAs on the reverse strand were not being masked before the protein coding sequence prediction step.

If you would like an existing analysis to be upgraded to version 4.1 of the pipeline, please get in touch via https://www.ebi.ac.uk/support/metagenomics.
