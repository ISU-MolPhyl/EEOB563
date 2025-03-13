## Lab 3 - Distance analysis with PHYLIP, and FastME 

In this lab we will learn about two phylogenetic programs that can be used for distance analysis

## Prerequisites:

### Login to Nova cluster
```
# Login
ssh yourname@nova.its.iastate.edu
# Also, request two cores for 2 hours
salloc -p instruction -N 1 -n 3 -t 120 -A s2025.eeob.563.1
```

### Update your EEOB563-Spring2023 git repository
- Go to the repository and pull the updates: `git pull origin master`

### Accessing the programs
- Both Phylip and FastME are installed as a modules on Nova (load with  `module load phylip` and `module load fastme`). You can also install them from their websites ([see links page](links.md))
- [Online version](http://www.atgc-montpellier.fr/fastme/) of fastme  is also available, but you should avoid it to practice your command line skills.  

### EMBOSS package
[EMBOSS](https://emboss.sourceforge.net/)  is a free Open Source software analysis package specially developed for the needs of the molecular biology user community.
It can be loaded as a module `module load emboss` or used [online](https://www.ebi.ac.uk/Tools/emboss/).
Among its many programs, you may be particularly interested in `seqret`, which does sequence conversion among various formats.
Here are a couple of examples:
```
### convert fasta alignment to nexus
seqret -sequence <input.fa> -outseq <output.nex> -osformat nexus/nexusnon
### convert fasta alignment to phylip
seqret -sequence <input.fa> -outseq <output.nex> -osformat phylip/phylipnon
```

## Lab tutorial

Lab 3: [PHYLIP, and FastME](lab3)

<!-- ## Additional tutorials

[Git/GitHub](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab1/git.pdf)  
[VI](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab1/vi_tutorial.pdf)  

-->

