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

### Week 11 (current)
* Midterm exam review and final project discussion
    * Be ready to present your final project outline.  Include hypotheses, data, and proposed methods for the project. 
    In addition, create a GitHub/GitLab repository for the final project and send me the link.

* Gene trees and species trees.
    * Reading: Allman and Rhodes (2016).  Chapter 13: Gene trees and species trees
    * Discussion: Copetti et al. 2017. Extensive gene tree discordance and hemiplasy shaped the genomes of North American columnar cacti. [Proc Natl Acad Sci U S A: 114: 12003-12008](http://www.pnas.org/content/114/45/12003.full).

... to be continued


---
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />Except where otherwise noted, content on this site is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
