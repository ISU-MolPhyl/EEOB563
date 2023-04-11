# Lab #7 Phylogenomics
The objective of this activity is to introduce you to main steps and approaches in phylogenomic analysis. 
We will use several programs for this exercise. 
A few of them will be familiar, but many will be novel. 
So be ready!

## Introduction
### What is phylogenomics?

The term “phylogenomics” refers to several areas of research at the interplay between genomics and evolution. 
Here we will use it in a sense of inferring species' relationships using genomic scale datasets.

### To concatenate or not to concatenate...

When dealing with the sequence data in phylogenomic analysis, one of the main decision we have to make is whether to concatenate the data. 
If **we do**, we can use any of the previously discussed phylogenetic methods to infer a species tree. 
It will just take longer. 
If **we don't**, we can use supertree or coalescent methods. 
We will try both approaches here.

### The dataset

We will use one of the dataset from the study by [McCormack et al. (2012)](http://www.genome.org/cgi/doi/10.1101/gr.125864.111). 
The directory for this lab contains both the sequences and alignments.

### Getting started

We will use several new programs in this excercise. 
All of them are already installed on Nova, but we'll do a few tricks to simplify their usage:

1. Login to Nova and request 4 cores for 2 hours:
```
salloc -p class-long -N 1 -n 4 -t 2:00:00 -A s2023.eeob.563.1
``` 

2. Edit your `.bashrc` file by running the following commands from your home (~) directory:
```
echo "alias amas='python3 /work/class-faculty/dlavrov/eeob563/bin/AMAS.py'" >> ~/.bashrc
echo "alias astral='java -jar /work/class-faculty/dlavrov/eeob563/src/ASTRAL/Astral/astral.5.7.8.jar'" >> ~/.bashrc
echo "alias pargenes='/work/class-faculty/dlavrov/eeob563/src/ParGenes/pargenes/pargenes.py'"  >> ~/.bashrc
echo "alias pargenes-export='python3 /work/class-faculty/dlavrov/eeob563/src/ParGenes/pargenes/pargenes_src/export.py'"  >> ~/.bashrc
source ~/.bashrc
```

## Part I: Concatenation-based analysis

We will use [AMAS](https://github.com/marekborowiec/AMAS) program to concatenate alignments present in the `data/org` directory. 
To run AMAS type `amas <command> [<args>]`. Running `amas` without a command provides this help guide:

```
usage: AMAS <command> [<args>]

The AMAS commands are:
  concat      Concatenate input alignments
  convert     Convert to other file format
  replicate   Create replicate data sets for phylogenetic jackknife
  split       Split alignment according to a partitions file
  summary     Write alignment summary
  remove      Remove taxa from alignment
  translate   Translate DNA alignment into protein alignment
  trim        Remove columns from alignment

Use AMAS <command> -h for help with arguments of the command of interest
```
1. Run the following commands from the lab7 directory:

```
mkdir -p analysis/{concatenation,coalescence};
cd analysis/concatenation;
amas concat -f nexus -d dna --out-format nexus --part-format nexus -i ../../data/org/183_aln/nexus/*.nex
```
The code above creates a concatenated alignment (`concatenated.out`) as well as
a list of individual loci locations in this alignment (`partitions.txt`)

2. Run your favorite program (e.g., MrBayes) to estimate a phylogenetic tree based
on the alignment. Note, use `out-format phylip` option if you want to create a
phylip-formatted file (e.g., for RAxML)

## Part II: Coalescence-based analysis using ASTRAL
### Making gene trees with PARGENE and RAXML-NG

Before running ASTRAL we need to build inidividual trees. We'll do this with `ParGenes`.

[ParGenes](https://github.com/BenoitMorel/ParGenes) is a parallel tool that takes as input a set of multiple sequence alignments (typically from different genes) and infers their corresponding phylogenetic trees.

Pargenes has many options that you can check [here](https://github.com/BenoitMorel/ParGenes/wiki/Command-line) or by running `pargenes --help`. 
We won't use most of them for this lab.

1. Run `ParGenes` with the following command:  
```
cd ../coalescence
pargenes -a ../../data/org/183_aln/phylip -o ./pargene_out -c 16 -d nt -R "--model GTR"
```

2. Run an export script that extracts ML trees from the output directory:
```
pargenes-export --best-ml-tree -i pargene_out -o pargene_export.out
```

3. Concatenate all trees in one file:
```
cat pargene_export.out/* > gene_trees.tre
```

### ASTRAL

ASTRAL is a java program for estimating a species tree given a set of unrooted
gene trees. ASTRAL is statistically consistent under multi-species coalescent
model (and thus is useful for handling ILS). The optimization problem solved by
ASTRAL seeks to find the tree that maximizes the number of induced quartet trees
in gene trees that are shared by the species tree. The optimization problem is
solved exactly for a constrained version of the problem that restricts the
search space. An exact solution to the unconstrained version is also implemented
and can run on small datasets (less than 18 taxa).

#### Installation  

The program is already installed in `/work/class-faculty/dlavrov/eeob563`, but you can dowload it from its [github repository](https://github.com/smirarab/ASTRAL/) or use the module `module load astral` (older version).

#### EXECUTION:
* ASTRAL is a java-based application, and should run in any environment (Windows, Linux, Mac, etc.) but you need `java` to run it.

<!-- 
4. On HPC-Class load `java` with these two modules:

```
module load dafoam/1.0
module load java/1.8.0_51
```
-->

If you created an alias above, run ASTRAL by just typing `astral`. 
Typing `astral --help` will show you a <long> list of options available in ASTRAL:

```
================== ASTRAL ===================== 

This is ASTRAL version 5.7.8

Usage:
  ASTRAL (version5.7.8) [--help] (-i|--input) <input file> [(-o|--output) <output
  file>] [(-q|--score-tree) <score species trees>] [(-t|--branch-annotate) <branch
  annotation level>] [(-b|--bootstraps) <bootstraps>] [(-r|--reps) <replicates>]
  [(-s|--seed) <seed>] [-g|--gene-resampling] [--gene-only] [(-k|--keep) <keep>]
...
```

##### Input:
* The input gene trees are in the Newick format  
* The input trees can have missing taxa, polytomies (unresolved branches), and multiple individuals per species.  
*  Taxon names cannot have quotation marks (`'` or `"`) or special characters (like `|`, `=`, `?`, `/`, and `\`) in the name.  

##### Output:
The output in is Newick format and gives:  
* the species tree topology,  
* branch lengths in coalescent units (only for internal branches or for terminal branches if that species has multiple individuals),  
* branch supports measured as [local posterior probabilities](http://mbe.oxfordjournals.org/content/early/2016/05/12/molbev.msw079.short?rss=1).  
* It can also annotate branches with other quantities, such as quartet support, as described in the [tutorial](astral-tutorial.md).

4. We can run `ASTRAL` as
```
astral -i gene_trees.tre -o astral.tre
# or
astral -i gene_trees.tre -o astral.tre 2> astral.log
 ```

### Viewing results of ASTRAL:

5. The output of ASTRAL is a tree in Newick format. Let's use this [server](https://itol.embl.de/) to look at it.

Using either this applications open the `astral.tre` file.

Reroot the tree at the correct node, which is always necessary, since the rooting of the ASTRAL trees is arbitrary and meaningless.

#### Branch length and support

* ASTRAL only estimates branch lengths for internal branches and those terminal branches that correspond to species with more than one individuals sampled.
* Branch lengths are in coalescent units and are a direct measure of the amount of discordance in the gene trees. As such, they are prone to underestimation because of statistical noise in gene tree estimation.   
* Branch support values measure the support for a quadripartition (the four clusters around a branch) and not the bipartition, as is commonly done.

<!--


Here, the main input is just a file that contains all the input gene trees in Newick format. The input gene trees are treated as unrooted, whether or not they have a root. Note that the **output of ASTRAL should also be treated as an unrooted tree**.

The test file that we are providing here is based on the [Song et. al.](http://www.pnas.org/content/109/37/14942.short) dataset of 37 mammalian species and 442 genes. We have removed 23 problematic genes (21 mislabeled genes and 2 genes we classified as outliers) and we have also re-estimated gene trees using RAxML on the alignments that the authors of that paper kindly provided to us.

The input gene trees can have polytomies (unresolved branches) since [version 4.6.0](CHANGELOG.md).

### Running on larger datasets:
We will now run ASTRAL on a larger dataset. Run:

```
java -jar astral.5.7.7.jar -i test_data/100-simulated-boot
```

The input file here is a simulated dataset with 100 sequences and 100 replicates of bootstrapped gene trees for 25 loci (thus 2,500 input trees). Note that ASTRAL finishes on this dataset in a matter of seconds.

A larger real dataset from the [1kp](http://www.pnas.org/content/early/2014/10/28/1323926111) dataset is also included. This dataset includes
424 genes from 103 species. Run:

```
java -jar astral.5.7.7.jar -i test_data/1KP-genetrees.tre -o test_data/1kp.tre 2> test_data/1kp.log
```

This takes about a minute to run on a laptop. On this dataset, notice in the ASTRAL log information that it originally starts with 11043 clusters in its search space, and using heuristics implemented in ASTRAL-II, it increases the search space slightly to 11085 clusters. For more challenging datasets (i.e., more discordance or fewer genes) this number might increase a lot.

### Running with unresolved gene trees

In our [ASTRAL-III paper](https://doi.org/10.1007/978-3-319-67979-2_4) we showed that contracting very low support branches (e.g., below 10% bootstrap support) from gene trees can improve accuracy somewhat.
Thus, we recommend removing very low support branches.

To contract low support branches, you can use many tools,  including the [newick utilities](htpp://cegg.unige.ch/newick_utils). If you have newick utilities installed, you can use

```
nw_ed  1KP-genetrees.tre 'i & b<=10' o > 1KP-genetrees-BS10.tre
```

To create a file `1KP-genetrees-BS10.tre` that includes the 1KP dataset with branches of 10% support or lower contracted. If you don't have newick utilities, don't worry. The contracted file is part of the ASTRAL distribution.

```
java -jar astral.5.7.7.jar -i test_data/1KP-genetrees-BS10.tre -o test_data/1kp-BS10.tre 2> test_data/1kp-bs10.log
```

Compare the species tree generated here with that generated with the fully resolved gene trees. You can confirm that the tree topology has not changed in this case, but the branch lengths and the branch support have all changed (and that they tend to both increase). By comparing the log files you can also see that after contracting low support branches, the normalized quartet score increases to 0.92321 (from 0.89467 with no contraction). This is expected as low support branches tend to increase not decrease discordance.

-->
