---
published: true
layout: post
title: MGnify Proteins release - 2026_07
category: spotlight
emg:
  text: Checkout the new MGnify Proteins release
  url: https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_07/
---
![MGnify Proteins Schematic]({{site.baseurl}}/assets/media/images/posts/mgnify-proteins-growth-2026-07.png){:width="400px"}
We're happy to announce a new release of the [MGnify Proteins database](https://www.ebi.ac.uk/metagenomics/proteins/). The [last release of the database](https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2024_04/) in April 2024 aggregated over 2.4 billion non-redundant protein sequences generated from publicly available metagenomic datasets. This latest release significantly increases the scale even further, with over 5.7 billion non-redundant protein sequences available.

The release also includes 1.6 billion cluster representatives computed by [DIAMOND/Linclust](https://github.com/bbuchfink/diamond)[^1] at 90% sequence identity (MGnify90). Three filtered down subsets originating from MGnify90 were also generated at 30% sequence identity, which we refer to collectively as "MGnify30". As with previous releases, the files for the release are available on our [FTP server](https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_07/), and this release is supported on the [MGnify Proteins Portal](https://www.ebi.ac.uk/metagenomics/proteins/). The [HMMER web server](https://www.ebi.ac.uk/Tools/hmmer/search/phmmer?database=mgnify30_c2) now also supports searches on the three MGnify30 subsets. 

<figure style="text-align: center;">
    <img src="{{site.baseurl}}/assets/media/images/posts/mgnify-proteins-schematic.png" alt="MGnify Proteins growth as of July 2026" style="width: 60%;float: none" id="fig-dataflow"/>
    <figcaption style="clear: both; text-align: justify; text-align-last: left;">
        <strong>Figure 1: </strong> The flow of data from biome-tagged reads, to assemblies analysed by MGnify, to their resulting protein sequences that make up the MGnify Proteins database. The Database is accessible in the same ways as before, with the addition of Parquet files available in the FTP.
    </figcaption>
</figure>

A significant update with this release is the generation of all MGnify Proteins data in the [Apache Parquet](https://parquet.apache.org/) file format, as part of a shift in how we plan to distribute MGnify Proteins files going forward. There are numerous advantages to this shift:

- Columnar data access: As Parquet is a columnar data format, certain query structures that are commonly used to search MGnify Proteins metadata become significantly faster, as only columns of interest need to be searched.
- Native schemas: Parquet stores metadata about each column within a file - including data types - much like a relational database. These schemas allow for a more explicit data structure, more robust data validation, and more efficient queries e.g. querying based on integer identifiers in a Parquet file vs flat-files without a schema like `.tsv`, the possibility of applying [Bloom filters](https://simple.wikipedia.org/wiki/Bloom_filter), etc.
- Native compression: Parquet is a compressed file format designed for efficient storage, with data types that help store data more efficiently.
- Partial reading: Partial reading makes it possible to query remote Parquet data without downloading the entire source file.

The ecosystem for working with Parquet is broad, with support in most major programming languages and tools like [DuckDB](https://duckdb.org/). The Parquet files for the MGnify database are available alongside the usual flat files on our [FTP server](https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_07/), and can be queried with DuckDB like this:

```sql
SELECT *
FROM 'https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_07/mgy_protein_sequences.parquet'
WHERE protein_id = 46;
```

<style>
.bordered-table, .bordered-table th, .bordered-table td {
  border: 1px solid #ccc;
  border-collapse: collapse;
}
.bordered-table th, .bordered-table td {
  padding: 6px 10px;
}
</style>

<div style="overflow-x: auto;" markdown="1">
| protein_id | full_length | sequence |
|-----------:|-------------|----------|
| 46         | true        | MAKEDNIEMQGTVLDTLPNTMFRVELENGHVVTAHISGKMRKNYIRILTGDKVTVELTPYDLSKGRIVFRSR |
{: .bordered-table}
</div>

Please see the [README](https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_07/README.md) for information about the schemas of each Parquet file, and our [documentation](https://docs.mgnify.org/src/docs/mgnify-proteins-parquet-queries.html) for examples of how to use them. More in-depth release statistics about the release can also be found [here](https://ftp.ebi.ac.uk/pub/databases/metagenomics/peptide_database/2026_07/STATS.md)

<div style="overflow-x: auto; width: 100%;">
  <div id="main_block" style="display: flex; gap: 10px; min-width: max-content;">
    <iframe src="{{site.baseurl}}/assets/media/images/posts/sunburst_2024_04.html" height="600" width="620" style="border:none; flex-shrink: 0;"></iframe>
    <iframe src="{{site.baseurl}}/assets/media/images/posts/sunburst_2026_07.html" height="600" width="620" style="border:none; flex-shrink: 0;"></iframe>
  </div>
</div>

[^1]: Buchfink BJ, Barbé É, Ashkenazy H, Reuter K, Kennedy JA, Drost HG, "Clustering the protein universe of life using DIAMOND DeepClust", Nature Methods 23, 724-727 (2026). doi:10.1038/s41592-026-03030-z