---
title: Bioinformatics pipelines and scripts
summary: A set of tools and templates for basic bioinformatics tasks
---
'
# Pipelines
- [Reference-based mapping](https://github.com/dhart31/bioinformatics/blob/master/ref_assembly/Snakefile): maps short or long reads to a reference genome with bowtie2 or minimap2, respectively. Handles Illumina and Oxford Nanopore data.
- [De novo assembly](https://github.com/dhart31/bioinformatics/blob/master/denovo_assembly/Snakefile): assembles short Illumina reads with Spades.
- [RNA-Seq](https://github.com/dhart31/bioinformatics/blob/master/rnaseq/Snakefile): performs read alignment with HiSAT2, as well as transcript assembly and quantification with stringtie. Also prepares input files for DESeq2.

# Scripts

- [Cleaning FASTA headers](https://github.com/dhart31/bioinformatics/blob/master/scripts/tidy_transcripts_fasta.pl): clean FASTA headers with regex
- [Counting bases](https://github.com/dhart31/bioinformatics/blob/master/scripts/count_bases.pl): calculates per-base totals/percentages of a fasta, distinguishing between repetitive and non-repetitive bases.
- [Plot coverage](https://github.com/dhart31/bioinformatics/blob/master/ref_assembly/scripts/plot_coverage.py): creates an interactive coverage plot from a set of bed files. Uses Bokeh.

# One-liners

- Get number of lines from a raw content URL

```
wget -q -O - [url here] | grep '>' | wc -l
```

- Get lengths of a fasta sequence
```
awk '/^>/ {if (len) print len; len=0; next} {len += length($0)} END {if (len) print len}' sequence.fasta
```

- Get basic statistics from a stream of numbers (e.g. fasta lengths). Requires [r-base](https://anaconda.org/conda-forge/r-base).
```
[cmd] | R -q -e 'x <-scan(file("stdin")); summary(x); sd(x)'
```