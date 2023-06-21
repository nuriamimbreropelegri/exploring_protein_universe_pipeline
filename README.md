# TFM
Scripts used for my master thesis "EXPLORATION PROTEIN UNIVERSE FOR THE IDENTIFICATION OF EVOLUTIONARY CONSERVED FRAGMENTS FOR PROTEIN DESIGN"
## 1. ANNOTATION OF ESM METAGENOMIC ATLAS SEQUENCES USING SCOPe
### ESM ATLAS
Download data from the high confidence subset called MGnify30 in foldseek format. It contains 36,986,627 million sequences (equivalent to 1TB size file).
[ESM atlas data](https://github.com/facebookresearch/esm/blob/main/scripts/atlas/v0/highquality_clust30/foldseekdb.txt) 
 ### SCOPE DATABASE
 Download data from ASTRAL SCOPe 2.08 genetic domain sequence subsets, based on PDB SEQRES records, with less than 40% identity to each other
 [SCOPe sequences](https://scop.berkeley.edu/downloads/scopeseq-2.05/astral-scopedom-seqres-gd-sel-gs-bib-40-2.05.fa)
 ### ALIGN DATABASES WITH MMSEQS 
 mmseqs search: Compares all sequences in the query database with all sequences in the
target database, using the prefiltering and alignment modules. MMseqs2 search supports
sequence/sequence searches. They query database is the high confidence subset MGnify30 of ESM atlas and the target database the ASTRAL SCOPe 2.08.
Documentation of MMseqs2 User Guide: [MMseqs user Guide](https://mmseqs.com/latest/userguide.pdf) 
Code used to compute the alignment: [Code for: 1. Annotation (a: alignment )](https://github.com/nuriamimbreropelegri/TFM/blob/main/Annotation%20of%20ESM%20atlas%20sequences)
### CREATE THE ANNOTATED ESM ATLAS DATABASE
1. Filter by e-value score <10^-5, HSSP curve and alignment lenght [1. Annotation: (b: Filtering)](https://github.com/nuriamimbreropelegri/TFM/blob/main/1.%20Annotation%20(b%3A%20filtering))
2. Create a database containing the sequence tag and the corresponding domain: [2. Annotation (c: Assigning a fold to ESM atlas sequences)](https://github.com/nuriamimbreropelegri/TFM/blob/main/1.%20Annotation%20(c%3A%20assigning%20a%20fold%20to%20ESM%20atlas%20sequences))
3. Create a database containing the tags and the sequences of those ESM atlas sequences that found a hit in SCOPe: [1. Annotation: d: Database with tags and sequences of the annotated ESM atlas sequences](https://github.com/nuriamimbreropelegri/TFM/blob/main/1.%20Annotation%20(d%3A%20database%20of%20annotated%20sequences))
## 2. ALL-AGAINST-ALL COMPARISON OF ESM ATLAS SEQUENCES
### COMPUTING THE ALIGNMENTS USING MMSEQS 
1. Compute an all-against-all alignment between all the annotated sequences from ESM atlas using MMseqs2 easy search: [2. All-against-all (a: MMseqs alignment)](https://github.com/nuriamimbreropelegri/TFM/blob/main/2.%20All-against-all%20alignment%20of%20ESM%20atlas)
### REMOVE ALIGNMENT FROM THE SAME FOLD
2. Remove alignment that correlate sequences from the same fold: [2. All-against-all (b: Filter by fold)](https://github.com/nuriamimbreropelegri/TFM/blob/main/2.%20All-against-all%20(b%3A%20Filter%20by%20fold))
### ADD FOLD 
3. Add fold information from each ESM atlas sequence (using the created database containing the sequence tag and the corresponding domain) in the alignment file:  [2. All-against-all (c: Add fold information)](https://github.com/nuriamimbreropelegri/TFM/blob/main/2.%20All-against-all%20(c%3A%20Add%20fold%20information))
### FILTER 
4. Filter by Filter by e-value score <10^-5, HSSP curve and alignment lenght: [2. All-against-all (d: Filtering)](https://github.com/nuriamimbreropelegri/TFM/blob/main/2.%20All-against-all%20(d%3A%20Filtering))
## 3. CLUSTERING THE FRAGMENTS
### ADD HIT ID
1. Add an index number to each alignment result representing the hit ID [3. Clustering (a: add hit ID)](https://github.com/nuriamimbreropelegri/TFM/blob/main/3.%20Clustering%20(a%3A%20add%20hit%20ID))
### RETRUCTURE THE ALIGNMENT DATABASE
2. Create a database restructuring the alignment ESM atlas sequence fragments database to enable effective clustering of the sequences. The initial format, containing pairwise alignments, is transformed into a new format where each sequence's name is placed on a separate line, accompanied by the fragments obtained from the alignment file. Fragments are defined by their positions within the sequence and the identification number of the hit alignment: [3. Clustering: (b: Restructure the alignment database)](https://github.com/nuriamimbreropelegri/TFM/blob/main/3.%20Clustering%3A%20(b%3A%20Restructure%20the%20alignment%20database))
### CLUSTER THE FRAGMENTS USING DBSCAN ALGORITHM
4. Implement DBSCAN algorithm to the new file to generate a dictionary of clusters for all sequence IDs in the alignment hits: [3. Clustering: (c: Clustering data using DBSCAN algorithm)](https://github.com/nuriamimbreropelegri/TFM/blob/main/3.%20Clustering%3A%20(c%3A%20Clustering%20using%20DBSCAN%20algorithm))
### ADD CLUSTER INFORMATION TO THE ALIGNMENT DATABASE
5. Using this dictionary of clusters, the database that containing all the pairwise alignments describing common fragments is modified. The modification of this dataset is based on the substitution of each sequence ID for a sequence ID that contains information about the cluster of the sequence in which each fragment belongs: [4. Clustering: (d: Add cluster information to the alignment database)](https://github.com/nuriamimbreropelegri/TFM/blob/main/3.%20Clustering%3A%20(d%3A%20Add%20cluster%20information%20to%20the%20alignment%20file))
## 3. NETWORK CONSTRUCTION OF THE EVOLUTIONARY CONSERVED FRAGMENTS IN THE PROTEIN UNIVERSE
1. Create a file containing the nodes of the graph. The nodes in the graph will be all the different protein sequence names in the alignment file: [3. Network (a: nodes in the network)]
