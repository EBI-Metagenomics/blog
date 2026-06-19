---
published: true
layout: post
title: MGnify Proteins release - 2026_05
category: tools
emg:
  text: Checkout the new MGnify Proteins release
  url: https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_05/
---
![MGnify Proteins Schematic]({{site.baseurl}}/assets/media/images/posts/mgnify-proteins-schematic.png)

We're happy to announce a new release of the [MGnify Proteins database](https://www.ebi.ac.uk/metagenomics/proteins/). The [last release of the database](https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2024_04/) in April 2024 aggregated over 2.4 billion non-redundant protein sequences generated from publicly available metagenomic datasets. This latest release significantly increases the scale even further, with over 5.7 billion non-redundant protein sequences available, including 1.6 billion cluster representatives computed by [DIAMOND/Linclust](https://github.com/bbuchfink/diamond). 

<figure>
    <img src="{{site.baseurl}}/assets/media/images/posts/mgnify-proteins-growth-2026.png" alt="MGnify Proteins growth as of 2026" style="width:100%;" id="fig-dataflow"/>
</figure>

Like with previous releases, the files for the release are available on our [FTP server](https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_05/). Given the scale of the database growth, this release is not yet supported on the [MGnify Sequence Search](https://www.ebi.ac.uk/metagenomics/sequence-search/search/phmmer), [MGnify Proteins Portal](https://www.ebi.ac.uk/metagenomics/proteins/), and [Google Cloud Public Dataset](https://docs.mgnify.org/src/docs/mgnify-proteins-big-query.html). We are working hard to update these resources to work in the newest release as soon as possible.

A significant update with this release is the generation of all MGnify Proteins data in the [Apache Parquet](https://parquet.apache.org/) file format, as part of a shift in how we plan to distribute MGnify Proteins files going forward. There are numerous advantages to this shift:

- Columnar data access: As Parquet is a columnar data format, certain query structures that are commonly used to search MGnify Proteins metadata become significantly faster, as only columns of interest need to be searched. Columnar data similarly allows for partial reading of remote files.
- Native schemas: Parquet stores metadata about each column within a file - including data types - much like a relational database. These schemas allow for a more explicit data structure, more robust data validation, and more efficient queries e.g. querying based on integer identifiers in a Parquet file vs flat-files without a schema like `.tsv`, the possibility of applying [Bloom filters](https://simple.wikipedia.org/wiki/Bloom_filter), etc.
- Native compression: Parquet is a naturally compressed file format, with data types allowing for more efficient storing of this data.
- Partial reading: Using tools like [DuckDB](https://duckdb.org/) that support partial reading on Parquet files, it is possible to make remote queries without downloading the entire source file, unlike with regular flat file formats like `.tsv`.

The Parquet files for the MGnify database are available alongside the usual flat files on our [FTP server](https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_05/). Please see the README (TODO: add link) for information about the schemas of each Parquet file, and our documentation (TODO: add link) for examples of how to use them.