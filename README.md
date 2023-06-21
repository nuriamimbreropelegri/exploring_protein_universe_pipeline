# TFM
Scripts used for my master thesis "EXPLORATION PROTEIN UNIVERSE FOR THE IDENTIFICATION OF EVOLUTIONARY CONSERVED FRAGMENTS FOR PROTEIN DESIGN"
# 1. ANNOTATION OF ESM METAGENOMIC ATLAS SEQUENCES USING SCOPe
## ESM ATLAS
Download data from the high confidence subset called MGnify30 in foldseek format. It contains 36,986,627 million sequences (equivalent to 1TB size file).
[ESM atlas data](https://github.com/facebookresearch/esm/blob/main/scripts/atlas/v0/highquality_clust30/foldseekdb.txt) 
 ## SCOPE DATABASE
 Download data from ASTRAL SCOPe 2.08 genetic domain sequence subsets, based on PDB SEQRES records, with less than 40% identity to each other
 [SCOPe sequences](https://scop.berkeley.edu/downloads/scopeseq-2.05/astral-scopedom-seqres-gd-sel-gs-bib-40-2.05.fa)
 ## MMSEQS 
 mmseqs search: Compares all sequences in the query database with all sequences in the
target database, using the prefiltering and alignment modules. MMseqs2 search supports
sequence/sequence searches. They query database is the high confidence subset MGnify30 of ESM atlas and the target database the ASTRAL SCOPe 2.08.
Documentation of MMseqs2 User Guide: [MMseqs user Guide](https://mmseqs.com/latest/userguide.pdf) 
Code used to compute the alignment: [Code for: 1. Annotation (a: alignment )](https://github.com/nuriamimbreropelegri/TFM/blob/main/Annotation%20of%20ESM%20atlas%20sequences)
## CREATE THE ANNOTATED ESM ATLAS DATABASE
1. Create a database containing 2 columns where in the first appears the tags of the ESM atlas sequences that found a hit in SCOPe and in the second one the corresponding fold or domain: [2. Annotation (b: assigning a fold to ESM atlas sequences)](https://github.com/nuriamimbreropelegri/TFM/blob/main/2.%20Annotation%20(b%3A%20assigning%20a%20fold%20to%20ESM%20atlas%20sequences))
2. Create a database containing the tags and the sequences of those ESM atlas sequences that found a hit in SCOPe: [1. Annotation: c: Database with tags and sequences of the annotated ESM atlas sequences](https://github.com/nuriamimbreropelegri/TFM/blob/main/1.%20Annotation%20(c%3A%20database%20of%20annotated%20sequences))
  

