---
published: true
category: spotlight
title: Anvi’o visualisations for refinement of Eukaryotic MAGs
layout: post
carousels:
  - images:
    - image: /blog/assets/media/images/posts/anvio/SRR12480113_metabat2_3_MERGED.svg 
    - image: /blog/assets/media/images/posts/anvio/ERR594347_concoct_23_MERGED.svg  
    - image: /blog/assets/media/images/posts/anvio/ERR594348_concoct_6_MERGED.svg 
    - image: /blog/assets/media/images/posts/anvio/ERR598996_concoct_100_MERGED.svg
    - image: /blog/assets/media/images/posts/anvio/ERR599001_concoct_34_MERGED.svg 
    - image: /blog/assets/media/images/posts/anvio/ERR599023_concoct_42_MERGED.svg
    - image: /blog/assets/media/images/posts/anvio/ERR599095_concoct_98_MERGED.svg
    - image: /blog/assets/media/images/posts/anvio/SRR5788032_concoct_67_MERGED.svg
---
In the coming months, we will be expanding MGnify Genomes to include eukaryotic genomes. Eukaryotic metagenome-assembled genome (MAG) generation relies on assemblies of metagenomic data, typically performed by metaSPAdes [Nurk *et al.* (2017)](http://www.genome.org/cgi/doi/10.1101/gr.213959.116) or MEGAHIT [Li *et al.* (2015)](https://doi.org/10.1093/bioinformatics/btv033). These tools are not biased toward specific organisms, however compared to prokaryotes, eukaryotic genomes are large, have more compositional variation and contain more repetitive regions, meaning they are complex to both assemble (with many fragments) and to generate MAGs. For example, during binning we have found that a single eukaryotic genome can be split across two MAG bins. To alleviate some of these challenges, EukCC2 [Saary *et al.* (2022)](https://doi.org/10.21203/rs.3.rs-1441815/v1) contains a bin-merging functionality that connects bins from the same taxa, using measures of genome completeness and having paired-end reads connecting the two bins to validate merging. Others have used co-assembly and co-binning of multiple samples to overcome this problem [Delmont *et al.* (2022)](https://doi.org/10.1016/j.xgen.2022.100123), but related samples are not always available, hence MGnify has adopted single-sample approaches. Nevertheless, the challenges posed by eukaryotic MAG generation afford the need for users to inspect the quality of our automatically generated eukaryotic MAGs.

As part of the [BlueRemediomics](https://blueremediomics.eu) project, we have been investigating how to leverage the Anvi’o [Eren *et al.* (2021)](https://doi.org/10.1038/s41564-020-00834-3) interactive interface for visualising genomes and their derived sample composition. Here, we share our prototype of Anvi’o visualisations of MGnify-generated eukaryotic MAGs. The eukaryotic MAGs were generated for the same datasets used in the [Marine v2.0](https://www.ebi.ac.uk/metagenomics/genome-catalogues/marine-v2-0) prokaryotic genome catalogue. Here the MAGs were generated for each study in the dataset, on a sample by sample basis. Subsequently, all the MAGs were de-replicated together to remove redundancy, resulting in 12 species-level clusters, 8 of which comprised more than one genome. These 8 species-representative genomes were taxonomically classified into two families of green algae from the order *Mamiellales*. For these 8 species clusters, we mapped the read sequences pertaining to each sample that produced a genome in the species cluster, onto the species-representative genome and compiled them into Anvi’o profiles. Figure 1 shows the prototypes.

Visual representation of the hierarchical clustering of contigs in a eukaryotic genome by sample composition can allow a user to identify contigs which map uniquely to a subset of samples - indicating potentially contaminated contigs. More information on refinement can be found in the [Anvi’o blogs](https://merenlab.org/2015/05/11/anvi-refine/).

{% include carousel.html height="100%" width="200%" duration="20" number="1" %}
**Figure 1. Hierarchical clustering of sample reads mapped to contig regions visualised with Anvi’o. The images are generated from Anvi’o profiles compiled from samples which contributed to genomes, mapped to 8 species representative eukaryotic MAGs. Access the interactive version here.**


The Anvi’o profiles for all 8 marine eukaryotic genomes can be found on the [MGnify FTP server](http://ftp.ebi.ac.uk/pub/databases/metagenomics/anvio_prototype/). To visualise them you will need to install Docker and run the commands below in the directory with the desired input genome:

```
docker pull meren/anvio:8
# start container
docker run --rm -it -v `pwd`:`pwd` -w `pwd` -p 8080:8080 meren/anvio:8
# in container
anvi-interactive -p ${GENOME_NAME}_MERGED/PROFILE.db -c ${GENOME_NAME}.db
```


This Anvi’o feature is still in development, and we welcome any feedback and suggestions on the prototypes via our [MGnify helpdesk](https://www.ebi.ac.uk/about/contact/support/metagenomics) or X account [@MGnifyDB](https://x.com/MGnifyDB). We aim to provide such Anvi’o eukaryotic MAG visualisations alongside eukaryotic genome catalogues.
