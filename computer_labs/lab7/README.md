# Lab #7: Taming the BEAST  
## Divergence Time Estimation using BEAST 2  

<img src="./img/beast2.png" align="right" hspace="10">

### Introduction  
[BEAST 2](https://www.beast2.org/) is a cross-platform program for Bayesian phylogenetic 
analysis of molecular sequences. It estimates rooted, time-measured phylogenies using 
various molecular clock models. It can be used as a method of reconstructing 
phylogenies but is also a framework for testing evolutionary hypotheses without 
conditioning on a single tree topology. BEAST 2 uses Markov chain Monte Carlo (MCMC) 
to average over tree space, so that each tree is weighted proportional to its posterior 
probability. BEAST 2 includes a graphical user-interface for setting up standard analyses 
and a suit of programs for analysing the results. A core aspect of the BEAST 2 design 
philosophy is to allow researchers to extend the core program without the involvement 
of the BEAST 2 developers. New methods are implemented as standalone packages that are 
developed and maintained separately of BEAST 2 itself.

<img src="./img/tbeast.png" align="right" hspace="10">
The tutorial we will follow today covers only a small part of BEAST's abilities. However,
there is a great resource, [Taming the BEAST](https://taming-the-beast.github.io/) that 
contains a comprehensive set of BEAST 2 tutorials in one location that can be used to 
learn more about the program.

The program has been originally described in PloS Comp. Biol. [article](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003537). A recent book ["Bayesian Evolutionary Analysis with BEAST"](https://www.amazon.com/Bayesian-Evolutionary-Analysis-Alexei-Drummond/dp/1107019656) covers theory behind the analysis in addition to the program itself.

### Getting Started  
#### Software  

[BEAST 2](https://www.beast2.org/) is available for Mac, Windows, and Linux. It is also installed on the HPC-class. 
It should be easier to use it on your own computer, because we use GUI programs to 
set up a parameters file and to analyse the results.


In addition, we will use [Tracer](http://tree.bio.ed.ac.uk/software/tracer/) and 
[FigTree](http://tree.bio.ed.ac.uk/software/figtree/), both of which have executables for Windows and Macs.

### Tutorial  
We will be using a [tutorial](https://taming-the-beast.github.io/tutorials/FBD-tutorial/FBD-tutorial.pdf) prepared by [Dr. Tracy Heath](http://phyloworks.org/) from our [department](http://www.eeob.iastate.edu/).

The data for these tutorial is available at the tutorial [GitHub site](https://taming-the-beast.github.io/tutorials/FBD-tutorial/). I also included them in the `lab7/data` directory in the GitHub repository for this class.

### Good Luck!  

