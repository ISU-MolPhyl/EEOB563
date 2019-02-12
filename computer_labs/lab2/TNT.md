# TNT (Tree analysis using New Technology)## IntroductionTNT is a parsimony program by Pablo Goloboff, Steve Farris, and Kevin Nixon that can:  

* analyse large data sets (i.e. 300-500 taxa)* in reasonable times (minutes to find a shortest tree, hours to produce a reliable consensus).The program is described in Goloboff PA, Farris JS, Nixon KC (2008).  TNT, a free program for phylogenetic analysis. Cladistics 24:774–786.The program is often used in the Cladistics community.
## Data file format  
TNT reads matrices in Hennig86 format, with some refinements.  Normally, the data will be included in a file. Character states may be IUPAC codes, digits (for morphological characters), ? (for missing data), or - (for gaps). Simple Nexus files can also be used with variable success. The basic format for data input is:

> xread
'optional title, starting and ending with quotes (ASCII 39)'  
nchar ntax  
Taxon0   0000000000  
Taxon1   0010111000  
Taxon2   1011110000  
Taxon3   1111111000  
.....  
TaxonN   1111111000  
;  '<- Note the semicolon (and the way you add comments)!'

`Seqret` program in EMBOSS can be used for formatting.

The data can be defined as DNA using the command `nstates dna;` or proteins `nstates prot;` in which case the IUPAC codes (including polymorphisms) are recognized and used throughout.  For 32 states, non-protein data, the symbols 0-9 and A-V indicate states 0-31.

## Commands
There are 150 different commands in TNT, which can be see with the `help` command:  

|  |  |  |  |  |  |  |  
| ---: | ---: | ---: | ---: | ---: | ---: | ---: |  
| absincl | agroup | alltrees | ancstates | apo | **bbreak** | beep 
| best | bground | blength | blocks | break | bsupport | ccode | 
| cdir | change | chkmoves | chomo | ckeep | cls | clbuffer | 
| cnames | collapse | comcomp | condense | constrain | costs | cscores | 
| cstree | dcomp | dmerge | drift | edit | echo | export | 
| fit | fillsank | force | freqdifs | help | hold | hybrid | 
| **ienum** | incltax | info | lintrees | **log** | keep | kleex | 
| length | lmark | lmbox | lmrealign | lquote | majority | matchtax | 
| map | minmax | mixtrees | mono | mrp | **mult** | mxram | 
| mxproc | naked | nelsen | nstates | outgroup | **procedure** | pause | 
| pcrprune | pfijo | piwe | pruncom | prunmajor | prunnelsen | pruntax | 
| prupdn | ptnt | qcollapse | qnelsen | quote | **quit** | randtrees | 
| ratchet | rcompl | rdir | rebuild | recons | report | reroot | 
| resample | resols | rfreqs | riddup | rseed | run | save | 
| screen | scores | **sectsch** | shortread | shpcomp | silent | slfwt | 
| slaveproc | smatrix | sort | sprdiff | subopt | svtxt | system | 
| tables | tagset | taxcode | taxlabels | taxonomy | taxname | tchoose | 
| tcomp | tequal | tfuse | tgroup | thanks | timeout | tnodes | 
| **tplot** | tread | **tsave** | tshrink | tsize | ttags | txtsize | 
| tzert | view | vversion | warn | watch | xcomp | xgroup | 
| xinact | **xmult**| xperm | xpiwe | xread | xwipe | unique | 
| unshared | usminmax | zzz | 

## Preliminaries
_First_, increase TNT memory usage to 1 GB or whatever is realistic and necessary: `mxram 1000;`. The default -- 16.78 Mbytes -- is too low for most tasks.

_Second,_ enter `nstates DNA` or `nstates protein`, respectively, if using sequence data. Enter `nstates NOGAPS` to treat gaps as missing data as opposed to an additional state. 

_Thrid_, use `taxname = ;` to use taxon names for terminal nodes.

_Finally_ `log [logfilename];` will keep the log of your analysis.  


## Basic heuristic analysis with `mult`
For relatively messy, but not very big data sets, the best algorithm consists of multiple random addition sequences plus TBR (RAS+TBR); this is invoked with the `mult` command. Further branch-swapping starting from the trees in memory ("RAM") can be used to find the additional trees.

<!-- Whether or not you are likely to have found the best trees, or all the tree islands, depends on the ease with which the algorithm converges to the minimum length found. For this reason, the program reports the number of replications that reached the best score found. The program also reports whether some replications had partial overflows of the tree file, in which case, some most parsimonious trees may not have been found during the search; --> 

>`procedure [filename];` or `p`  will read the file;  
`hold 100000;` 
`mult;` will do a basic analysis consisting of 10 random addition of sequences followed by branch-swapping with TBR, saving up to 10 trees per replication.  
`bbreak=tbr;` 

The info about the program can be printed with `help mult;`, while parameters can be seen with `mult:;` and changed with `mult:options;`  Once calculated, trees may be viewed by entering `tplot`. To save the trees for later reanalysis, create a file by entering `tsave * [tree_filename]`. 

## More complex search with xmult

There are four basic types of special algorithms implemented in TNT: ratchet, drifting, sectorial searches, and fusing.  

**The ratchet** (`ratchet`) consists of two phases, perturbation and search, which are sequentially repeated.  The ratchet always uses TBR branch swapping, and it alternates the search phase (S) with three types of perturbation phase: original weights (O), upweighting (U), and deleting (D). 

<!-- During the perturbation phase, rearrangements of score equal or better than the tree being swapped are always accepted, untill a certain number of rearrangements have been made (or untill a certain percentage of the total swapping on the tree has been completed). 

<!-- This seems to provide better results than the original ratchet. The "autoconstrained" option calculates the (strict) consensus of the previous tree and the tree resulting from the rearrangement phase, and during the subsequent search phase, only rearrangements that do not violate monophyly of the shared groups are done.  The rationale for this is that improvements are likely to be found in areas that have changed during the perturbation phase.  Every certain numer of constrained cycles, an unconstrained search phase is done (to insure global optimality).  If this is used in combination with user-defined constraints, both are combined. -->

**Tree-drifting** (`drift`) is similar to the ratchet, but the perturbation phase, instead of reweighting the characters, accepts the moves with a probability that depends on both the relative fit difference and the absolute fit difference between the tree being swapped and the new tree. The perturbation phase also alternates between acceptance of optimal trees only (O), and suboptimal trees (U): O,S,U,S,O,S,U… etc.

<!-- It has the advantage that memory managing is easier, and for that reason is the only perturbator that sectorial-searches (see below) can use. The perturbation phase also alternates between acceptance of optimal trees only (O), and suboptimal trees (U): O,S,U,S,O,S,U… etc. Any of the O or U phases can be skipped (the O phase, with drift:noequal; or with the skip optimal-only drifting option in the tree-drift settings dialog box; the U becomes effectively an O by setting the score difference to a very low number). -->

<!-- Sectorial-searches are of two basic types: constraint-based and random; a combination of both is the mixed sectorial searches.  -->

**Sectorial searches** (`sectsch`) take a portion of the tree, create a reduced data set, and produce a mini-analysis of that data set.  If a better solution for that portion of the tree is found, it is replaced back into the original tree. Every certain number of (user-determined) rearrangements, a round of global TBR is done (to insure global optimality).  

<!-- If the sectors are below a certain size, the mini-analysis consists of three RAS+TBR (random addition sequence wagner trees plus TBR); if the three sequences end up in trees of the same score, the mini-analysis is interrupted (i.e. the reduced data is "clean" and not worth of further analysis); otherwise, three additional RAS+TBR are done.  If the sectors are above that size, a certain number of iterations of tree-drfiting is done to the reduced sector.  The three types of sectorial-search differ in how the sectors are selected.  Constraint-based searches choose the sectors by reference to constraints: the nodes that are resolved as polytomies in the constraint tree, connecting to no less than N branches (where N is some number defined by the user; default is 10). A reduced data sets corresponding to each of the polytomies in the constraint tree is analyzed, in turn; this is repeated a certain number of times (default=3), because changing some sector may imply that other sectors should change as well.  Random sectors are chosen at random, to be no smaller and no bigger than a certain (user defined) size. The mixed sectorial searches use both constraint-based and random sectors; they can only be used with multiple addition sequences.  For the mixed sectorial search, a temporary constraint tree is created by consensing the tree found at some stage of the present addition sequence (user defined: this can be the wagner tree, which is the default, or optionally the tree produced by SPR or TBR), and this constraint tree is used to do a constraint-based sectorial search.  Once this is finished, a random sectorial search is done (unconstrained, or using only the user-defined constraints if they are in effect). -->

**Tree-fusing** (`tfuse`) mixes trees, producing better trees. If the trees comes from different searches, the score is often considerably improved in very short time.  

<!-- Tree-fusing produces (so to speak) a synergistic effect for all those previous searches; this also means that the rate of score improvement is not necessarily lineal (i.e. all the searches before fusing were not producing a score improvement beyond some bound, but were nonetheless accumulating "momentum" for the subsequent fusing). -->

These algorithms are implemented in the `xmult` command.  The default for the command are:
  
* Using 4 replications as starting point for each hit 
* Each replication initially autoconstrained (previous and wagner) 
* Each replication with constraint and random sectorial searches, with no ratchet, with drifting (5 iters.), no hybridization, and fusing (1 rounds) 
* Finding best score 1 times (=hits)
* Not consensing trees during search
* Multiplying trees by fusing after hitting best score
* Saving no more than 1 trees per replication 

One way to modify:
`xmult=hits 10 noupdate nocss replic 10 ratchet 10 fuse 1 drift 5 hold 100 noautoconst keepall;`


>A careful consideration of how the data set behaves to changes in parameters is the best way to proceed, but if you have no idea of how a data set behaves, or don't know how to set the parameters for a search, you may trust to the program the choice of parameters.  This is done with the `level` option of the `xmult` command).  The level must be a number between 0 and 10 (0 is very superficial; 10 is extremely exhaustive).  If using a driven search (i.e. more than a single hit of the xmult command), you may have the program check whether best score is being found easily or not (and then decrease or increase the search level accordingly).  This is set with the `chklevel` option of the `xmult` command.

## Measures of character support
 
<!--TNT implements two types of character support measures: Bremer supports and resampling.  The Bremer supports are calculated from the trees in memory: it is up to the user to find suboptimal trees.  The resampling can be of different types, some of which are preferrable to others.  Standard bootstrapping is influenced by uninformative characters (and by characters irrelevant to monophyly of a given group).  Bootstrapping (both standard and Poisson) and jacknifing (except for a resampling probability of 50%) are affected by character weight and transformation costs (e.g. additive characters).  Symmetric resampling is affected by none.  Outputting results with the frequency may produce alterations in the apparent support for groups with very low support (and it cannot measure support for groups with very low support).  Both GC and frequency slopes solve this problem (for slopes, supported groups have negative slopes; the closer to 0, the better supported the group).  The supports can be measured on the groups present in any given tree (normally, a most parsimonious tree, but using other trees provides a way to measure how strongly contradicted some groups are).  The slopes must be measured by reference to a pre-existing tree.

If some taxon has its position in the tree very poorly defined, it may strongly decrease the support for many groups in the tree.  If you wish to find out whether the rest of the tree is well supported, you can eliminate the taxon from the consensus when resampling.  To find out which taxon is floating around you may have to first do a more superficial estimation, saving the trees, and trying to prune different taxa (note that in such case you have to take the precaution of not collapsing the trees with SPR or TBR, as otherwise you may never find the floating taxon: once you found it, you turn collapsing back to SPR or TBR –the most effective—and do a more careful estimation of the resampling frequencies eliminating the evil terminals).

Usually you will name your save file with a .tre extension. -->
If there are multiple trees, their strict consensus can be found by entering `nelsen`. Resampling (jackknifing, bootstrapping, etc.) can be done by entering `resample.`  
Now download the file cox1_nt.tnt to your working directory and try this command: `tnt p cox1_nt.tnt, echo=, log cox1_nt.out, rep+1, mu10=ho3, le, ne, resample, quit,`

Trees were produced and analysed in TNT 1.5-beta (Goloboff et al. 2008). In total 74 taxa were
scored for 457 characters. Using the new technology search function, with ratchet and drift set to
their defaults (10 iterations and 10 cycles respectively) and with 100 random additional sequences,
our data produced 93 MPTs of length 1734. Bremer supports were also calculated using TNT 1.5-
beta. 
