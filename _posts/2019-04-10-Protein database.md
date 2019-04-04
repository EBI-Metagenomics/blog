---
published: false
layout: post
title: The MGnify protein database: searching the microbial dark matter
category: tools
emg:
  text: Search protein database
  url: https://www.ebi.ac.uk/metagenomics/sequence-search/search/phmmer
---
![Dark matter]({{site.baseurl}}/assets/media/images/posts/ico_code_EMG_grey.png)
The MGnify protein sequence database comprises sequences predicted from assemblies generated from publicly available metagenomic datasets. The initial release in August 2017 comprised just under 50 million sequences; the current version contains in excess of 800 million. All sequences now have stable accessions.

As well as providing the files on our [FTP][ftp-server] server, we have used [HMMER][hmmer-website] to provide sequence searches against this dataset. While we were initially able to provide searches against the full catalogue, the database growth has outpaced the compute resources required to make this feasible. To address this, searches are now restricted to a set of representative sequences obtained by clustering the full set based on sequence identity using [Linclust][linclust-paper]. The representative sequences nevertheless capture the diversity of the data, and the full database remains available via FTP. We have also added files which describe how the sequences are clustered.

We have added new options to the search page. In addition to the ability to search against full length proteins (from complete genes) or partial proteins (predicted to extend beyond the length of the assembled contig), users can now refine searches according to the top level environment/biome from which the matching sequences were derived. The results page has also been improved. Users can now access matched sequences directly by clicking on their accessions. Links to all matching MGnify samples and runs are also provided, along with links to any identical matching sequences in UniProtKB. An option to highlight full length sequence matches is also provided. For more information, see the README on the FTP server or our [documentation][documentation].

[ftp-server]:        ftp://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database
[hmmer-website]:     http://hmmer.org/
[linclust-paper]:    https://www.nature.com/articles/s41467-018-04964-5
[documentation]:     https://emg-docs.readthedocs.io/en/latest/sequence-search.html