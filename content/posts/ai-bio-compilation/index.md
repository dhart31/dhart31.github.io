---
title: "A timeline of BioML"
date: 2024-06-29
showToc: true
summary: ""
---

Keeping track of the stream of ML applications in biology (for better or worse)
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
