# Lab #5: Bayesian analysis
## Bayesian phylogenetics with MrBayes
<img src="./bayes_neon.jpg" align="right" hspace="10">
### Introduction
Bayesian inference in phylogeny (also called Bayesian phylogenetics) is based upon a quantity called the posterior probability distribution of trees, which is the probability of a tree given the observations (alignment of sequences) and the model. The conditioning is accomplished using Bayes's theorem. As the posterior probability distribution of trees is impossible to calculate analytically, phylogenetic programs using Bayesian approach (such as MrBayes or PhyloBayes) use a simulation technique called Markov chain Monte Carlo (or MCMC) to approximate the posterior probabilities of trees.

### The goal

The goal of this lab is to introduce you to MrBayes, one of the two major software packages for conducting Bayesian phylogenetic analysis (the other being BEAST, which we'll see later). 

### Getting Started.
#### Software

`MrBayes` is installed as a module (called mrbayes) on HPC-class. To use run:  
`module load mrbayes;  
salloc -N 1 -n 4 -t 2:00:00;  
mpirun -np 4 mb`

You can also install it on your computer from the [GitHub](https://github.com/NBISweden/MrBayes). In addition, we will use [Tracer](http://tree.bio.ed.ac.uk/software/tracer/) and 
[FigTree](http://tree.bio.ed.ac.uk/software/figtree/), both of which have executables for Windows as well as Macs.

#### Data
The data for this exercise is in the directory data on GitHub repository.


### Tutorial
Now go to the [tutorial](./MrBayes.md).