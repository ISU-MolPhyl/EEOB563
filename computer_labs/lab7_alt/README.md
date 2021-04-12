# Lab #6 Phylogenomics
The objective of this activity is to introduce you to main steps and approaches in
phylogenomic analysis.

## Introduction
### What is phylogenomics?

The term “phylogenomics” refers to several areas of research at the interplay
between genomics and evolution. Here we will use it in a sense of
inferring species' relationships using genomic scale datasets.

### To concatenate or not to concatenate...

When dealing with the sequence data, one of the main decision we have to make is
whether to concatenate our data. If **we do**, we can use any of the previously
discussed phylogenetic methods to infer a species tree. If **we don't do it**,
we can use supertree or concatenation methods. We will do both in this lab.

### The dataset

We will use one of the dataset from the study by [McCormack et al. (2012)](http://www.genome.org/cgi/doi/10.1101/gr.125864.111) that we have already seen in the Gatesy and Springer's paper.
The directory for this lab contains both the sequences and alignments.

## Part I: Concatenation-based analysis

We will use a subset of alignments found in `exercise1` directory. We will
concatenate them using the [AMAS](https://github.com/marekborowiec/AMAS) program.

1. You can clone github repository for AMAS in your home directory. Alternatively,
use the one installed in `/shared/class/eeob563`. I recommend adding the following
alias to your `.bashrc` file for convenience by running two commands:

```
echo "alias amas='python3 /shared/class/eeob563/src/AMAS/amas/AMAS.py'" >> ~/.bashrc
source ~/.bashrc
```

2. Now we can concatenate the sequences:
```
# from the lab7 directory
mkdir -p analysis/{concatenation,coalescence};
cd analysis/concatenation;
amas summary -f nexus -d dna -i ../../data/reduced/*.nex #just to show you another command :)
amas concat -f nexus -d dna --out-format nexus --part-format nexus -i ../../data/reduced/*.nex
```

The code above creates a concatenated alignment (`concatenated.out`) as well as
a list of individual loci locations in this alignment (`partitions.txt`)

3. Run your favorite program (e.g., MrBayes) to estimate a phylogenetic tree based
on the alignment.

## Part II: Coalescence-based analysis using ASTRAL
ASTRAL is a java program for estimating a species tree given a set of unrooted
gene trees. ASTRAL is statistically consistent under multi-species coalescent
model (and thus is useful for handling ILS). The optimization problem solved by
ASTRAL seeks to find the tree that maximizes the number of induced quartet trees
in gene trees that are shared by the species tree. The optimization problem is
solved exactly for a constrained version of the problem that restricts the
search space. An exact solution to the unconstrained version is also implemented
and can run on small datasets (less than 18 taxa).

### Installation  

* You can download the program using one of two approaches:
    * You simply need to download the [zip file](https://github.com/smirarab/ASTRAL/raw/master/Astral.5.7.7.zip) and extract the contents to a folder of your choice.
    * Alternatively, you can clone the [github repository](https://github.com/smirarab/ASTRAL/).
* I install the program in `/shared/class/eeob563`. You can create an alias to simply its usage:

```
echo "alias amas='python3 /shared/class/eeob563/src/AMAS/amas/AMAS.py'" >> ~/.bashrc
source ~/.bashrc
```

### EXECUTION:
* ASTRAL is a java-based application, and should run in any environment (Windows, Linux, Mac, etc.) but you need java to run it. So you need to load two modules:

```
module load dafoam/1.0
module load java/1.8.0_51
```

If you created an alias, run ASTRAL by just typing `astral`. Typing command
without any arguments will give you a list of options available in ASTRAL.

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

### Making gene trees with PARGENE and RAXML-NG

[ParGenes](https://github.com/BenoitMorel/ParGenes) is a parallel tool that takes
as input a set of multiple sequence alignments (typically from different genes)
and infers their corresponding phylogenetic trees.

Run `ParGenes` with the following command:
```
```

Now run an export script that extracts ML trees from the output directory:
```
```

### Viewing results of ASTRAL:

The output of ASTRAL is a tree in Newick format. These trees can be viewed in many existing tools. Here are some that are used by many people:

1. [FigTree](http://tree.bio.ed.ac.uk/software/figtree/) is probably the most widely used tool. It produces nice looking figures and works under Linux, Windows, and MAC.
2. [Archaeopteryx](https://sites.google.com/site/cmzmasek/home/software/archaeopteryx) is very good for viewing large trees and also works under all three operating systems.
3. [EvolView](http://www.evolgenius.info/evolview): online application. You don't even need to download.

There are [many more tools](http://en.wikipedia.org/wiki/List_of_phylogenetic_tree_visualization_software).

For this tutorial, let's use the online viewer (EvolView) or any other tool you can manage to download and install. Using either of these applications open the `test_data/song_mammals.tre` file. We will explore various tree viewing options. Importantly, we will reroot the tree at the correct node, which is always necessary, since the rooting of the ASTRAL trees is arbitrary and meaningless.

There have been some reports that FigTree and some other tools sometimes have difficulty opening ASTRAL trees. This is likely because ASTRAL does not generate terminal branch lengths. In the case of FigTree, opening the three two or three times in a row often works (who knows why!). In other tools, you may have to add an arbitrary branch length to each branch. [This script](https://github.com/smirarab/global/blob/master/src/mirphyl/utils/add-bl.py) may be of help.  

### Branch length and support

ASTRAL measures branch length in coalescent units and also has a fast way of measuring support without a need for bootstrapping.
The algorithms to compute branch lengths and support and the meaning of support outputted is further described in [this paper](http://mbe.oxfordjournals.org/content/early/2016/05/12/molbev.msw079.short?rss=1).
We will return to these in later sections. Some points have to be emphasized:

* ASTRAL only estimates branch lengths for internal branches and those terminal branches that correspond to species with more than one individuals sampled.
* Branch lengths are in coalescent units and are a direct measure of the amount of discordance in the gene trees. As such, they are prone to underestimation because of statistical noise in gene tree estimation.   
* Branch support values measure the support for a quadripartition (the four clusters around a branch) and not the bipartition, as is commonly done.



### The ASTRAL Log information

ASTRAL outputs lots of useful information to your screen ([stderr](https://en.wikipedia.org/wiki/Standard_streams), really). You can capture this information
by directing your stderr to a file. Capturing the log is highly recommended. Here is how you would capture stderr:

```
java -jar astral.5.7.7.jar -i test_data/song_mammals.424.gene.tre -o test_data/song_mammals.tre 2> song_mammals.log
```

Here are some of the important information captured in the log:

* Number of taxa, and their names. Double check these to make sure they are correct.
* Number of genes.
* Version of ASTRAL used in your analysis.
* The normalized quartet score (proportion of input gene tree quartet trees satisfied by the species tree). This is a number between zero and one; the higher this number, the *less* discordant your gene trees are.
* The final optimization score is similar to the above number, but is not normalized (the number of gene tree quartets satisfied by the species tree).
* Running time.
* More advanced info: the size of the search space in terms of the number of clusters and number of tripartitions (i.e., elements weighted).  

Scoring existing trees
---

You can use the `-q` option in ASTRAL to score an existing species tree to produce its quartet score, compute its branch lengths, and compute its ASTRAL branch support values. The ASTRAL score is the fraction of the induced quartet trees in the input set that are in the species tree. So, a score of `0.9` would mean that 90% of the quartet trees induced by your gene trees are in your species tree.

To score a tree using ASTRAL, run:

```
java -jar astral.5.7.7.jar -q test_data/simulated_14taxon.default.tre -i test_data/simulated_14taxon.gene.tre -o test_data/simulated_scored.tre 2> test_data/simulated_scored.log
```

This will score the species tree given in `test_data/simulated_14taxon.default.tre` with respect to the gene trees given in `test_data/simulated_14taxon.gene.tre`. It will output the following in the log:

```
Quartet score is: 4803
Normalized quartet score is: 0.4798201798201798
```

This means 4803 induced quartet trees from the gene trees are in the species tree, and these 4803 quartets are 47.98% of all the quartet trees that could be found in the species tree. As mentioned before, this dataset is one with a *very high* ILS level.

In addition to giving an overall score, when you score a tree, branch lengths
and branch support are also computed and outputted. In the next section, we will
introduce ways to output even more information per branch.

* When scoring a tree, you probably want to capture the stderr using `2>name_of_a_file` redirection, as described before.

* Just like the use of ASTRAL for inferring species trees, you can combine `-a` and `-q` to compute branch support values for multi-individual dataset.  

Extensive branch annotations
--

Whether you are inferring a species tree or scoring one using the `-q` option, you will always get estimates of the branch length and local posterior support for each branch.
In addition to these default annotations for each branch, you can ask ASTRAL to output other per branch information.

**Three Possible Rearrangements:**
Around each branch in an unrooted tree, there are four groups. If you think about a rooted tree, the four groups defined by a branch are the first child (`L`), the second child (`R`), the sister group (`S`), and everything else (`O`). With these four groups, if we keep all the groups intact, we can have three unrooted topologies: `RL|SO`, `RS|LO`, and `RO|LS`. The first topology is what the
current tree has, and we refer it to as the main topology. The two others
are alternative topologies, and we refer to `RS|LO` and `RO|LS` as the first and the second alternatives, respectively. ASTRAL can output branch annotations for the main tree as well as the two alternatives.

* When the output includes annotations for alternative topologies, we always first show the main topology, followed by `RS|LO` and `RO|LS`, in that order.

* Note: a common question I get is how do I know which child is `L` and which child is `R`. Unfortunately, the answer depends on your tree viewing software. There is no general rule.
	* You can always look at the newick file directly, and the first child is `L` and the second is `R`; thus, in the output newick format, we always have
`(LEFT,RIGHT)`.
	* But most people would find this cumbersome. Instead, you can look at options `-t 16` and `-t 32` [below](#file-export-of-branch-annotations) that output a `.csv` file.

**`-t` option**:
To enable extra per branch information, you need to use the `-t` option, and various types of information that can be turned on. Most `-t` options just annotate the newick file. Some of the will also turn on the output of the `.csv` file mentioned earlier.






### Introduction
PAML is *a package* of programs for phylogenetic analyses of DNA or protein sequences using maximum likelihood. It is maintained and distributed for academic use free of charge by Ziheng Yang. Examples of analyses that can be performed using the package include:  

* Comparison and tests of phylogenetic trees (`baseml` and `codeml`);  
* Estimation of parameters in sophisticated substitution models
 (`baseml` and `codeml`);  
* Likelihood ratio tests of hypotheses through comparison of implemented models (`baseml`,
`codeml`, `chi2`);  
* Estimation of divergence times under global and local clock models (`baseml` and `codeml`);  
* Likelihood (Empirical Bayes) reconstruction of ancestral sequences using nucleotide, amino acid and codon models (`baseml` and `codeml`);  
* Generation of datasets of nucleotide, codon, and amino acid sequence by Monte Carlo
simulation (`evolver`);  
* Estimation of synonymous and nonsynonymous substitution rates and detection of positive
selection in protein-coding DNA sequences (`yn00` and `codeml`).
* Bayesian estimation of species divergence times incorporating uncertainties in fossil calibrations (`mcmctree`).

The strength of PAML is its collection of sophisticated substitution models.  Tree search algorithms implemented in `baseml` and `codeml` are rather primitive, so except for very small data sets with say, <10 species, you are better off to use another package, such as phylip, paup, or mrBayes, to infer the tree topology.  You can get a collection of trees from other programs and evaluate them using `baseml` or `codeml` as user trees.

### Getting Started.
#### Software

PAML is alredy installed on the HPC-class (module paml). To use it, run:  

```
salloc -N 1 -n 4 -t 2:00:00;  
module load paml;  
name_of_the_paml_program
```

You can also install PAML on your computer from its [website](http://abacus.gene.ucl.ac.uk/software/paml.html){:target="_blank"}.

*Note:* For the exercises below we will use a single program from the paml package: `codeml`.

#### Data
The data for this exercise is in the `lab6` directory on the GitHub repository.

### Exercise 1: ML estimation of the dN/dS (ω) ratio “by hand”
####  Running on the sample mammalian dataset

We will next run ASTRAL on an input dataset. From the ASTRAL directory, run:

```
java -jar astral.5.7.7.jar -i test_data/song_mammals.424.gene.tre
```

The results will be outputted to the standard output. To save the results in an output file use the `-o` option:

```
java -jar astral.5.7.7.jar -i test_data/song_mammals.424.gene.tre -o test_data/song_mammals.tre
```

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

### Running on a multi-individual datasets

When multiple individuals from the same species are available, to force the species to be monophyletic, a mapping file needs to be provided using the `-a` option. This mapping file should have one line per species, and each line needs to be in one of two formats:

```
species_name [number of individuals] individual_1 individual_2 ...

species_name:individual_1,individual_2,...
```
Some rules about the mapping file:

* When multiple individuals exist for the same species, your species names should be different from the individual names.
* You cannot have empty names (e.g., `,,`)
* The same individual name should not be mapped to multiple species
* Each individual name should appear in at least one gene name

For example, you can run

```
java -jar astral.5.7.7.jar -i test_data/1KP-genetrees.tre -o test_data/1KP-speciestrees-multiind.tre -a test_data/namemap-1kp.txt 2> test_data/1kp-speciestree-multiind.log
```

Interpreting output
-----
