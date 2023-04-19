# Lab #8: BayesTraits  
## Evolutionary Inference with BayesTraits  

<img src="./img/baboons.jpg" align="right" hspace="10">
The objective of this activity is to help you understand how to conduct comparative analysis using Maximum Likelihood and Bayesian approaches. 
The exercises come from various versions of the [BayesTraits manual](http://www.evolution.reading.ac.uk/BayesTraitsV4.0.1/Files/BayesTraitsV4.0.0-Manual.pdf) and have been adapted to the current version fo the program (Version 4.0.1).  
Additional exercises can be found at the AnthroTree [website](https://wiki.duke.edu/display/AnthroTree/AnthroTree+Home).

## Introduction
[BayesTraits](http://www.evolution.reading.ac.uk/BayesTrees.html) is a computer package written by Andrew Meade and Mark Pagel for performing analyses of trait evolution among groups of species for which a phylogeny or sample of phylogenies is available. 
It can be applied to the analysis of traits that adopt a finite number of discrete states, or to the analysis of continuously varying traits. 
Hypotheses can be tested about models of evolution, about ancestral states, and about correlations among pairs of traits.

### Getting Started  
#### Software  

[BayesTraits](http://www.evolution.reading.ac.uk/SoftwareMain.html) is available for Mac, Windows, and Linux. 
I pre-installed two version of the program on Nova: the standard build (`BayesTraits`) and the Threaded version (`BT4-multi`).
The latter version will utilize all the cores you've requested with the `-n` option below. 
You have to request resource allocation (`salloc -p class-long -N 1 -n 4 -t 2:00:00 -A s2023.eeob.563.1`) before you use the program.

#### Datafiles
We will be using several datasets in this lab (all available in data directory on GitHub):  

* `Primates.trees`: sampled topologies from a Bayesian analysis, 
   where all but the first 20 trees have been removed;  
* `MatingSystems.txt`: a file with a list of primate species and 
   their mating systems. For purposes of this example primate mating 
   systems were classified as "1": multimale (females mate with 
   more than one male) or "0": unimale/monogamous.
* `Primates.txt`: same as `MatingSystems.txt`, except an additional column with presence/ absence of oestrous advertisement (sexual swellings) in female primates is added. 
* `Mammal.trees`: a sample of 50 mammal trees 
* `MammalBody.txt`: a data file with corresponding body size (the mammalian trees and data are for illustrative purposes and are not accurate or a good sample).

### Tutorial
Now go to the [tutorial](./BayesTraits.md).
