# Molecular Phylogenetics - Spring 2018

## Iowa State University -- EEOB 563

A graduate course on the theory and practice of phylogenetic analysis

**Instructor:** [Dennis Lavrov](https://sites.google.com/site/dennislavrov/)

**Time/Location:** Tuesday and Thursday, 9:00-10:50 AM in 203 Bessey Hall 

**Web View:** [https://isu-molphyl.github.io/EEOB563-Spring2018](https://isu-molphyl.github.io/EEOB563-Spring2018/)

## Reading Material

* [*Lecture Notes: The Mathematics of Phylogenetics*](https://jarhodesuaf.github.io/PhyloBook.pdf) by [E. S. Allman]() & [John A. Rhodes](https://jarhodesuaf.github.io/)

## Software Requirements

We will be using UNIX and Git throughout the course. If you are a Linux or MacOS user, you already have these tools installed.
If you are a Windows user, see the [installation guide](https://isu-molphyl.github.io/EEOB563-Spring2018/install) for instructions on installing.  
In addition, we will be using multiple phylogenetic programs in this class. All of them are free and most of them are already installed on the HPC-Class.
If you want to install them on your computer, use the links provided [here](https://isu-molphyl.github.io/EEOB563-Spring2018/links).

## Course Schedule

The topics covered in this course can all be found here: [Spring 2018 Schedule](https://sites.google.com/site/eeob563/schedule2018).
Be sure to check the schedule for updates.

## Syllabus

A copy of the course syllabus can be found at the following link: [Spring 2018 Syllabus](https://sites.google.com/site/eeob563/syllabus). A pdf is also available in this GitHub repository.

### Week 1
* Lecture 1: Introduction to Molecular Phylogenetics [[slides](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/01_09_18.pdf)]  
    * Reading: Allman and Rhodes (2016).  Chapter 2: Combinatorics of Trees I.  
    * Discussion: Baum et al. (2005). The Tree-Thinking Challenge.  Science 310: 979-980.  

* Lecture 2: Trees and characters [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/01_11_18.pdf)]

### Week 2
* Lecture 3: Homology and Sequence Alignment [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/01_16_18.pdf)]
    * Reading: Lemey, Salemi and Vandamme, Chapters 3: 3.1-3.10.  
    * Discussion: Fitch (2000). Homology a personal view on some of the problems. TIG 16: 227.
* [Computer Lab 1](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab1): Introduction to Unix/GitHub/SSH  
    * All users, make sure you have a GitHub account!
    * Windows users, please see the [installation guide](https://isu-molphyl.github.io/EEOB563-Spring2018/install) for instructions on installing a command-line tool.
* [Assignment 2](https://isu-molphyl.github.io/EEOB563-Spring2018/assignments/assignment2.pdf) (**due 01/25**)

### Week 3  
* Lecture 4: Parsimony and cladistics. Optimality criteria and character optimization.  
    * Reading:  Allman and Rhodes (2016).  Chapter 3: Parsimony. [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/01_23-25_18.pdf)] 
* Lecture 5: Searching tree space. Measures of character fit. Assessing clade support.  
    * Reading: Allman and Rhodes (2016).  Chapter 9: Tree Space. [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/01_23-25_18.pdf)] 
    * Discussion: Baron et al. (2017). A new hypothesis of dinosaur relationships and early dinosaur evolution. [Nature 543: 501-506](https://www.nature.com/articles/nature21700). 
    See also [News & Views](https://www.nature.com/articles/543494a). 

### Week 4  
* [Computer Lab 2](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab2): Multiple Sequence Alignment and Parsimony analysis.
    * All users, make sure you have a GitHub account!
    * You may want to install ClustalW, Mafft, PAUP*, and TNT on your computer [[links](https://isu-molphyl.github.io/EEOB563-Spring2018/links)]. Alternatively, you can use HPC-class cluster.
* Lecture 6: Distance matrix methods. Clustering algorithms. [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/02_01-02_06.pdf)]
    * Reading: Allman and Rhodes (2016).  Chapter 5: Distance Methods.
    * Discussion: Naxerova et al. (2017). Origins of lymphatic and distant metastases in human colorectal cancer. [Science 357, 55-60](http://science.sciencemag.org/content/357/6346/55).
* [Assignment 3](https://isu-molphyl.github.io/EEOB563-Spring2018/assignments/assignment3.pdf) (**due 02/06**)

### Week 5
* Lecture 7: Clustering algorithms (cont.). Model-based distances. [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/02_01-02_06.pdf)]
    * Reading: Reading: Allman and Rhodes (2016).  Chapter 6: Probabilistic Models of DNA Mutations. 
    * Reading: Reading: Allman and Rhodes (2016).  Chapter 7: Model-based Distances.
* [Computer Lab 3](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab3): Distance analysis with PHYLIP and FastME.
* [Assignment 4](https://isu-molphyl.github.io/EEOB563-Spring2018/assignments/assignment4.pdf) (**due 02/15**)  

### Week 6
* Lecture 8: Introduction to Maximum Likelihood. [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/02_13-15_18.pdf)]
    * Reading: Allman and Rhodes (2016).  Chapter 8: Maximum Likelihood.
* Lecture 9: Constructing Phylogenetic Trees Using Maximum Likelihood. [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/02_13-15_18.pdf)]
    * Discussion: Pittis and Gabaldón (2016). Late acquisition of mitochondria by a host with chimaeric prokaryotic ancestry. [Nature 531: 101-104](https://www.nature.com/articles/nature16941).
    See also [News & Views](https://www.nature.com/articles/nature16876)

### Week 7 
* [Computer Lab 4](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab4): Likelihood analysis in FastML and RAxML.
* [Assignment 5](https://isu-molphyl.github.io/EEOB563-Spring2018/assignments/assignment5.pdf) (**due 02/27**)

* Lecture 10: Bayes’ theorem and Bayesian methods in phylogenetics. [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/02_22-27_18.pdf)]
    * Reading: Allman and Rhodes (2016).  Chapter 12: Bayesian Inference.

### Week 8
* Lecture 11: Applications of Bayesian methods. [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/02_22-27_18.pdf)]
    * Discussion: Zaremba-Niedzwiedzka et al. (2017). Asgard archaea illuminate the origin of eukaryotic cellular complexity. [Nature, 541:353-358](https://www.nature.com/articles/nature21031).
    See also [News & Views](https://www.nature.com/articles/nature21113).
* Lecture 12: Model selection and model averaging in Likelihood and Bayesian methods.
    * Reading and Discussion: Posada and Buckley 2004.  Model selection and model averaging in phylogenetics: 
    advantages of Akaike Information Criterion and Bayesian Approaches over Likelihood Ratio tests. [Systematic Biology, 53:793–808](https://academic.oup.com/sysbio/article/53/5/793/2842928).

### Week 9 
* [Computer Lab 5](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab5): Bayesian analysis with MrBayes.
* [Assignment 6](https://isu-molphyl.github.io/EEOB563-Spring2018/assignments/assignment6.pdf) (**due 03/27**)[[dataset]](https://isu-molphyl.github.io/EEOB563-Spring2018/assignments/hiv.nxs)

* **03/08 Midterm Exam**
    * Review reading: Yang and Rannala (2012). Molecular phylogenetics: principles and practice. [Nature Review Genetics, 13:303-314](https://www.nature.com/articles/nrg3186.pdf)

### Week 10: Spring Break! 
* Don’t forget about your project outline! (**due 3/20**)

### Week 11 
* Midterm exam review and final project discussion
    * Be ready to present your final project outline.  Include hypotheses, data, and proposed methods for the project. 
    In addition, create a GitHub/GitLab repository for the final project and send me the link.

* Lecture 13 (ha!): Gene trees and species trees.
    * Reading: Allman and Rhodes (2016).  Chapter 13: Gene trees and species trees
    * Discussion: Copetti et al. 2017. Extensive gene tree discordance and hemiplasy shaped the genomes of North American columnar cacti. [Proc Natl Acad Sci U S A: 114: 12003-12008](http://www.pnas.org/content/114/45/12003.full).

### Week 12 
* Lecture 14: Neutral and adaptive protein evolution [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/03_27_18.pdf)].
    * Reading: Bielawski and Yang (2000). Statistical methods for detecting molecular adaptation.  [TREE 15(12): 496-503](http://www.cell.com/trends/ecology-evolution/abstract/S0169-5347(00)01994-7).
    * Discussion:  Tenaillon et al. (2016). Tempo and mode of genome evolution in a 50,000-generation experiment. [Nature 536: 165-170](https://www.nature.com/articles/nature18959).

* [Computer Lab 6](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab6): Hypotheses testing with PAML.

### Week 13 
* Lecture 15: Timing the evolutionary events [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/04_03_18.pdf)].
    * Reading: Sauquet (2013). A practical guide to molecular dating. [C. R. Palevol 12. 355–367](https://www.sciencedirect.com/science/article/pii/S1631068313001097)
    * Discussion: Worobey et al. (2016). 1970s and ‘Patient 0’ {HIV}-1 genomes illuminate early {HIV}/{AIDS} history in North America. [Nature 539: 98-101](https://www.nature.com/articles/nature19827).

* [Computer Lab 7](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab7): Taming the BEAST.

### Week 14 (Current)
* Lecture 16: Ancestral State Reconstruction and Comparative tests [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/04_10_18.pdf)].
    * Reading: Pagel and Meade (2006).  Bayesian Analysis of Correlated Evolution of Discrete Characters by Reversible-Jump Markov Chain Monte Carlo.  Am. Nat. 167:808-825.
    * Discussion: Watts et al. 2016. Ritual human sacrifice promoted and sustained the evolution of stratified societies. [Nature 532: 228-231](https://www.nature.com/articles/nature17159).

* [Computer Lab 8](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab8): BayesTraits.
    * Reading (again): Pagel and Meade (2006).  Bayesian Analysis of Correlated Evolution of Discrete Characters by  Reversible-Jump Markov Chain Monte Carlo.  Am. Nat. 167:808-825.
    * **Final project draft due:** share your GitHub/GitLab address with two assigned reviewers.  Perform the kind of positive, constructive review you would like to get on your own draft.  Prepare your reviews by 4/17.  

### Week 15 
* Lecture 17: Phylogenomics and the tree of life <!--- [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/04_10_18.pdf)].--->
    * Reading: Delsuc et al. 2005.  Phylogenomics and the reconstruction of the tree of life.  Nature Reviews.  Genetics.  6: 361-375. <!--- Need to change --->
    * Discussion: Watts et al. 2016. Simion et al. (2017). A Large and Consistent Phylogenomic Dataset Supports Sponges as the Sister Group to All Other Animals. Current biology 2: 958-967.

* Lecture 18: Signal vs. noise in phylogenetic reconstruction <!--- [[notes](https://isu-molphyl.github.io/EEOB563-Spring2018/lecture_notes/04_10_18.pdf)].--->.
    * Discussion: Philippe et al. 2017. Pitfalls in supermatrix phylogenomics. [European Journal of Taxonomy 283: 1-25](http://www.europeanjournaloftaxonomy.eu/index.php/ejt/article/view/407).

    
* **Revised final project due on 4/22 at 11:59pm (commit to GitHub and email me the link)**

### Final Presentations:
* 04/24: 9:00-10:50am
* 04/26: 9:00-10:50am
* 05/02: 7:00-9:00pm  

---
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />Except where otherwise noted, content on this site is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
