---
title: "A timeline of BioML"
date: 2024-06-29
showToc: true
summary: ""
---

Keeping track of the ongoing stream of ML applications in biology (for better or worse)

## March 5, 2025: [Prohormone prediction uncovers a non-incretin anti-obesity peptide](https://www.nature.com/articles/s41586-025-08683-y#Sec13)

## Data
The computational side of this project extracted canonical sequences from reviewed, secreted human genes retrieved from UniProtKB (an EMBL-EBI and SIB consortium). The resulting fasta was fairly small (~2000 records). However, these sequences were not training data; the subsequent bioactivity prediction tools relied on several academic, manually-curated peptide datasets: APD3, BioDADPep, BIOPEP-UWM, CancerPPD, CAMPR3, DBAASP, LAMP2, NeuroPedia, NeuroPep, PeptideDB, and SATPdb. 

## Model
The bioactivity step uses neural network models [MultiPep](https://pmc.ncbi.nlm.nih.gov/articles/PMC8665375/) and [PeptideRanker](https://pmc.ncbi.nlm.nih.gov/articles/PMC3466233/), both convolutional neural networks. 

Multipep's starting conv. layers range from 4-40 amino acids. These are pooled and churned through iterations of dense+dropout. The resulting outputs are used to predict a peptide class hierachy w/ some simple sigmoid or max operations. PeptideRanker is entirely different: it scans a window across the peptide, applying a 2 layer NN to each window chunk. These are summed together, and fed through another 2 layer NN.  

## February 19, 2025: Evo 2

### Data
This uses [OpenGenome2](https://huggingface.co/datasets/arcinstitute/opengenome2/tree/main), a curated set of fastas with 8.8 trillion nucleotides. 

- Eukaryotic reference genomes (~17k organisms), metagenomes, mRNA and ncRNA are from [NCBI RefSeq](https://www.ncbi.nlm.nih.gov/refseq/) and others (e.g. EMBL-EBI).

- Prokaryotic reference genomes (~113k organisms) are from [GTDB](https://gtdb.ecogenomic.org/) (which is itself sourced from NCBI RefSeq)

### Model

Evo2 uses [StripedHyena2](https://arcinstitute.org/manuscripts/Evo2-ML), a "hybrid" model with both explicit and implicit convolutional operators. The blocks of convolutional operators are interleaved by vanilla multi-head attention layers. The selling point of "hybrid models" is subquadratic computational costs without comprising, similar to other transformer alternatives.

## February 19, 2025: AI co-scientist

### Data

This is an "agent" system built on Gemini 2.0; the training data for this LLM, like all big tech models, is not public. They are also scant on details about the databases used by the agent tools. In their supp. examples, they list [TCGA](https://www.cancer.gov/ccg/research/genome-sequencing/tcga) (an NIH program), [Open Targets Platform](https://platform.opentargets.org/downloads) (EMBL, Sanger, and pharma are partners), [DepMap](https://depmap.org/portal/data_page/?tab=overview)(a Broad institute project), and Alphafold, which uses [PDB](https://www.rcsb.org/) as a database. I understand agents are pitched as a framework that can be linked to any database, but I still would have liked a list of what they use now.

### Model
The paper states that a team of specialized agents underpin the model. An [agent](https://www.kaggle.com/whitepaper-agents) is tech marketing-speak for an LLM embedded in a runtime along with a toolset, memory, etc. The more rigorous thinking is outsourced to focused, intentionally designed scientific models (eg Alphafold)

Perhaps the most notable agent is the ranking agent, which uses competitive strategies like self-play/tournaments. They do mention that the ranking agent uses auto-evaluated ELO or expert assessments to compare hypotheses; hence the rankings are not based on objective ground truth (their words, not mine). In fairness, they do say that they want "more objective, less intrinsically-favored evaluation metrics". I suspect those metrics will turn out to be ... experimental results.

## January 7, 2025: [Nationwide real-world implementation of AI for cancer detection in population-based mammography screening](https://www.nature.com/articles/s41591-024-03408-6#Sec10)

### Data

This study (PRAIM), which claims to be the largest to use AI for mammography screenings, uses 2 million images, 10% of which were annotated by radiologists. Approximately half a million women participated in the subsequent screening study, with 260k assigned to the AI-supported double reading group. 

Associated with each examination, they also collected a set of [metadata](https://datadryad.org/dataset/doi:10.5061/dryad.zs7h44jgn#readme).

### Model

The programme used a proprietary software created by [Vara](https://www.vara.ai/praim). There is not much detail given on the image processing model, beyond a comment that it consists of a combination of deep convolutional neural networks. Regardless, the image scores are joined with associated priors in an aggregation model. A clever ethical strategy of Vara's tech is to optimize for both specificity and sensitivity and incorporate them both into the examination flowchart. 