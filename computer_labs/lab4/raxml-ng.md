# RAxML-NG tutorial
**IMPORTANT NOTE**: This tutorial describes the functionality of the latest
[RAxML-NG v1.2.2](https://github.com/amkozlov/raxml-ng)
and is based on the [tutorial](https://github.com/amkozlov/raxml-ng/wiki/Tutorial)
provided by its authors.

<!--
* [Intro](#intro)
* [Getting help](#getting-help)
* [Preparing the alignment](#preparing-the-alignment)
* [Tree inference](https://github.com/amkozlov/raxml-ng/wiki/Tutorial#tree-inference)
* [Bootstrapping](https://github.com/amkozlov/raxml-ng/wiki/Tutorial#bootstrapping)
* [Tree likelihood evaluation](https://github.com/amkozlov/raxml-ng/wiki/Tutorial#tree-likelihood-evaluation)
* [Partitioned analysis](https://github.com/amkozlov/raxml-ng/wiki/Tutorial#partitioned-analysis)
* [Advanced Tutorial](https://github.com/amkozlov/raxml-ng/wiki/Advanced-Tutorial)
-->
## Intro
RAxML-NG replaces standard RAxML as well as the corresponding supercomputer
version ExaML. 
RAxML-NG does not (yet) support all options of standard RAxML,
so you may need to use the [previous implementation](https://cme.h-its.org/exelixis/web/software/raxml/index.html) for some tasks.

### Before you start:
* I already installed RAxML-NG in the class directory
* You can still update the course repository to download the data files

Check that you have the RAxML-NG version 1.2.2 or later:

```
$ raxml-ng -v

RAxML-NG v. 1.2.2-master released on 30.04.2024 by The Exelixis Lab.
Developed by: Alexey M. Kozlov and Alexandros Stamatakis.
...
```

## Getting help
#### `--help` option displays the help menu (you can also run `raxml-ng` without parameters).

More comprehensive documentation is available in [GitHub wiki](https://github.com/amkozlov/raxml-ng/wiki).

## Data and Model
Remember that likelihood is the probability of the data given the model (P(D|M)).  
So we have to specify our data and our model in all `raxml-ng` commands.

#### `--msa <FILE>` option (required) specifies alignment
RAxML-NG supports alignments in FASTA, PHYLIP and CATG formats.
By default, RAxML-NG will try to automatically detect alignment format based on
the file contents. You can also specify the alignment format explicitly with the
`--msa-format` option.

#### `--model <MODEL>` option (required) specifies the model of evolution.
Examples of possible models are `GTR+G` for nucleotide data, `JTT+G` for aa data,
`BIN` for binary data, `MULTI8_MK` multistate data with 8 categories, among
[many others](./models.md).

## Output
#### `--prefix <NAME>` option (optional) addes prefix to output files.
RAxML-NG will generate several output files. Use the `--prefix <NAME> ` option
to avoid over-writing them.

## Checking/optimizing your data

#### Use the `--check` command to check/optimize your dataset.

`--check` command checks that the MSA can actually be read and doesn't contain
sites with only undetermined characters or sequences with undetermined characters
or duplicate taxon names, etc. etc. If the problems are found, a "cleaned" file
is written.

```
raxml-ng --check --msa <DATAFILE> --model <MODEL> --prefix T1
```

#### Use the `--parse`	command for large alignments

In addition to MSA check, `--parse` command will perform two useful operations:

1. Compress alignment patterns and store MSA in the binary format
2. Estimate memory requirements and optimal number of CPUs/threads

```
raxml-ng --parse --msa <DATAFILE> --model <MODEL> --prefix T2
```

## Running ML search
#### `--search` conducts a heurstic search for the ML tree
By default, `--search` will perform 20 tree searches using 10 random and 10
parsimony-based starting trees, and pick the best-scoring topology. You can add
the `--seed <N>` option for reproducibility.

```
 raxml-ng --msa <DATAFILE> --model <MODEL> --prefix T3 --threads 2 --seed <N>
```

#### `--tree pars{N},rand{M}` option specifies the number of starting trees
Although, the default settings is a reasonable choice for many practical cases,
computational resources permitting, we might want to increase the number of
starting trees to explore the tree space more thoroughly:

```
 raxml-ng --msa <DATAFILE> --model GTR+G --prefix T4 --threads 2 --seed 2 --tree pars{25},rand{25}
```
Conversely, we can perform a quick-and-dirty search from a single random starting
tree using the `--search1` command:

```
 raxml-ng --search1 --msa <DATAFILE> --model GTR+G --prefix T5 --threads 2 --seed 2
```
#### `--rfdist` computes topological Robinson-Foulds (RF) distances among the trees

You may wonder if 20 (or even 50) starting trees were enough for the analysis. The program's ouput showed some variation in the Final logLikelihood values, but was it due to different
topologies? We can check this by using the `--rfdist` command to compute the
topological Robinson-Foulds (RF) distance among all trees:  

```
raxml-ng --rfdist --tree mltrees --prefix RF
```  
Use `cat` to examine the `.rfDistances` file.

## Bootstrapping

**NOTE:** As of v. 0.8.0b, RAxML-NG supports only *standard/slow* bootstrap
algorithm (`-b` option in RAxML8). It is much slower than *rapid* bootstrapping
implemented in RAxML8 (`-x` or `-f a` options), but gives more accurate support values estimates.

#### `--bootstrap` performs non-parametric bootstrap analysis.

```
raxml-ng --bootstrap --msa <DATAFILE> --model GTR+G --prefix T7 --seed 2 --threads 2
```

By default, RAxML-NG will perform [MRE-based bootstopping test](https://www.liebertpub.com/doi/abs/10.1089/cmb.2009.0179) after every 50 replicates, and terminate once the diagnostic
statistics drops below the cutoff value.

However, you can manually specify the number of replicates with the
`--bs-trees <N>` option, where N is the number of replicates.

Bootstrap convergence can also be checked post-hoc using the `--bsconverge`
command, we can also change the cutoff value to make the test more or less stringent:
```
raxml-ng --bsconverge --bs-trees <BOOTSTRAPS> --prefix T9 --seed 2 --threads 2 --bs-cutoff 0.01
```

#### `--support` maps bootstrap values on the ML tree

We can map bootstrap values onto the best-scoring/best-known ML tree.
We will use the ML tree obtained in the run `T3`:

```    
raxml-ng --support --tree T3.raxml.bestTree --bs-trees allbootstraps --prefix T13 --threads 2
```  

We can use a tree viewer (I use FigTree a lot) to visualize the ML tree with mapped bootstrap values (you have to choose "label" option under the "display node support".

>**Tip:** To view a phylogenetic trees on the terminal, use the `nw_display` program from the `newick_utils` package.

<!-- However, you'll need to use the older RISA modules:
>
```
module unuse /opt/rit/spack-modules/lmod/linux-rhel7-x86_64/Core
module use /opt/rit/modules
module load newick_utils
```
-->

Alternatively, we can compute so-called *Transfer Bootstrap Expectation* support metric [(Lemoine et al. 2018)](https://www.nature.com/articles/s41586-018-0043-0), which is supposedly more appropriate for very large trees:   

```
raxml-ng --support --tree T3.raxml.bestTree --bs-trees allbootstraps --prefix T14 --threads 2 --bs-metric tbe
```

## Running ML search and bootstrap analysis in one step
#### `--all` command runs both ML search and bootstrap analysis;
* `--bs-metric` option maps these bootstrap values on the ML tree.  

```  
raxml-ng --all --msa <DATFILE> --model <MODEL> --prefix T15 --seed 2 --threads 2 --bs-metric fbp,tbe
```

## Tree likelihood evaluation

Was it worth doing the ML analysis?  Wasn't the parsimony/distance tree good enough?

One way to answer these question is to compute the likelihoods of MP, NJ, and ML trees by just optimizing model and/or branch length parameters and not changing the topology itself.

#### `--evaluate` command calculates likelihood of a tree
* `--opt-model on/off` you can enable/disable model parameter optimization.
* `--opt-branches on/off` you can enable/disable branch length optimization.

The commands looks like:
```
raxml-ng --evaluate --msa <ALIGNMNET> --threads <N> --model <MODEL> --tree <TREE TO EVALUATE> --prefix <PREFIX>
```

## Partitioned analysis
#### Use `--model <file_name>` to specifies partitions.
So far, we used a single evolutionary model for all sites in our alignment. 
This is rather unrealistic biologically, because different genes and/or codon positions typically exhibit distinct substitution patterns. 
Therefore, it is common to divide alignment sites into subsets or *partitions*, which can be assigned individual evolutionary models. 
In the simplest case, we can assign identical *models* for all partitions, but allow independent *model parameter* estimates. 
For example, the dataset we'll use today can be partitioned by individual genes as encoded in the following file:  

```
GTR+G+FO, cob=1-1248
GTR+G+FO, cox1=1249-2808
GTR+G+FO, cox2=2809-3543
GTR+G+FO, cox3=3544-4482
```

A more sophisticated paritioning may involve different substitution matrices and rate heterogeneity models, and also split genes by codon position:  

```
GTR+G+FO, COB=1-1248
GTR+G+FO, COXp1_2=1249-4482/3,1250-4482/3
HKY, COXp3=1251-4482/3
```
### Beware of branch lengths
#### `-brlen` option sets the branch linkage model

In partitioned analyses, there are three common ways to estimate branch lengths (sometimes called *branch linkage* modes):

- **linked**: all partitions share a common set of (global) branch lengths. This is the simplest model with fewest parameters (`#branches`). However, it is often considered too unrealistic, since it is known that genes (or genome regions) evolve at different speeds.
- **unlinked**: each partition has its own, independent set of branch lengths. This model allows for the highest flexibility, but it also introduces a huge number of free parameters (`#branches * #partitions`), which makes it prone to overfitting.
- **scaled** (**proportional**): a global set of branch lengths is estimated like in `linked` mode,  but each partition has an individual scaling factor; per-partition branch lengths are obtained by multiplying the global branch lengths with these individual scalers. This approach is a compromise that allows to model distinct evolutionary rates across partitions while introducing only a moderate number of free parameters (`#branches + #partitions`).

## Topological constraint
#### `--constraint-tree FILE` option specifies a constraint tree

If the constraint tree is _comprehensive_ (i.e., it includes all taxa found in the MSA), then RAxML will simply resolve polytomies in the way that maximizes the likelihood. Conversely, if some taxa are missing from the constraint, they will be placed freely in the resulting ML tree.

## Outgroup rooting
#### `--outgroup  o1,o2,..,oN` option specifies outgroups when drawing a tree

The outgroup can be a single taxon (`--outgroup Human`) or a list of taxa which form a monophyletic group (`--outgroup Human,Chimp,Gorilla`).

*Please note that outgroup rooting is just a drawing option and will not affect tree inference process or score in any way!*

## Now it is your turn.
**1)** Find the ML tree for the provided dataset using the GTR + gamma model of sequence evolution and calculate bootstrap support using 50 bs replicates.

**2)** Calculate the likelihood score for the following models of DNA evolution: Jukes-Cantor (JC), JC with rate heterogeneity (JC+G), GTR (GTR), GTR with the Gamma model of rate heterogeneity, but empirical base frequencies (GTR+G+FC), same buth with ML estimate of the base frequencies (GTR+G+FO), as previously by with 4 free rates instead of GAMMA-distributed rates (GTR+R4+FO). Use the best tree from above and E1-E6 prefixes for these analyses.

Check the results with:  
```
$  grep logLikelihood E*.raxml.log
```
> What did you find?

Check AIC/BIC scores with
```
grep "AIC score" E*.raxml.log
```
> What model had the best (smallest) AIC/BIC score?

**3)** Does it make more sense to partition by gene or by codon position? (use your best tree to evaluate).  Use the best partitioning scheme to infer the ML tree.  Does it have a different topology from your original tree.


**4)** Which of the *branch linkage* modes has the highest likelihood?  Which one should we choose (use your best tree to evaluate). Use the best model to search for the ML tree.  Did it change the resulting likelihoods and/or topology?

<!--
```
raxml-ng --msa prim.phy --model prim.part --prefix P5 --threads 2 --seed 2 --brlen scaled
```
```
raxml-ng --msa prim.phy --model prim.part --prefix P6 --threads 2 --seed 2 --brlen linked
```
```
raxml-ng --msa prim.phy --model prim.part --prefix P7 --threads 2 --seed 2 --brlen unlinked
```
Checking the new likelihood scores
```
grep "Final LogLikelihood" {P5,P6,P7}.raxml.log
```
```
P5.raxml.log:Final LogLikelihood: -5672.951995
P6.raxml.log:Final LogLikelihood: -5678.301081
P7.raxml.log:Final LogLikelihood: -5648.204296
```
-->
<!--However, there is some evidence that the choice of DNA substitution models has rather limited influence on the resulting tree topology [(Hoff et al. 2016)](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-016-0985-x). This does not mean that we can ignore model selection altogether. But probably we should not worry too much about subtle details such as `AIC(c)` vs. `BIC` conflicts or sample size definition.-->

# What's next?

There is more info in the [Advanced Tutorial](https://github.com/amkozlov/raxml-ng/wiki/Advanced-Tutorial)!
