---
title: "A timeline of BioML"
date: 2024-06-29
showToc: true
summary: ""
---

## February 19, 2025: Evo 2

### Data
This uses [OpenGenome2](https://huggingface.co/datasets/arcinstitute/opengenome2/tree/main), a curated set of fastas with 8.8 trillion nucleotides. 

- Eukaryotic reference genomes (~17k organisms), metagenomes, mRNA and ncRNA are from [NCBI RefSeq](https://www.ncbi.nlm.nih.gov/refseq/) and others (e.g. EMBL-EBI).

- Prokaryotic reference genomes (~113k organisms) are from [GTDB](https://gtdb.ecogenomic.org/) (which is itself sourced from NCBI RefSeq)

### Model

Evo2 uses [StripedHyena2](https://arcinstitute.org/manuscripts/Evo2-ML), a "hybrid" model with both explicit and implicit convolutional operators. The blocks of convolutional operators are interleaved by vanilla multi-head attention layers. The selling point of "hybrid models" is subquadratic computational costs without comprising, similar to other transformer alternatives.
