# Evolutionary model

Option: `--model STRING | FILE` _(mandatory)_

Evolutionary model can be specified globally (i.e., for the whole alignment), or multiple models can be selected for different subsets of alignment columns (so called *partitioned analysis*).

### Single model
Global per-alignment evolutionary model can be given as a string on the command line.
Model specification always starts with a substitution matrix name, e.g., `GTR` for DNA data or `LG` for protein data. 
Several optional modifiers can be added, separated by `+` and in arbitrary order.

**NOTE**: all per-state values (e.g. base frequencies) must be given in the [following order](https://github.com/amkozlov/raxml-ng/wiki/Input-data#state-encoding--order).

All substitution matrices and modifiers are summarized in the following table:

|          Modifier      |    Possible values |
|------------------------|--------------------|
| Substitution matrix<br>| **DNA data**: `JC`, `K80`, `F81`, `HKY`, `TN93ef`, `TN93`, `K81`, `K81uf`, `TPM2`, `TPM2uf`, `TPM3`, `TPM3uf`, `TIM1`, `TIM1uf`, `TIM2`, `TIM2uf`, `TIM3`, `TIM3uf`,`TVMef`, `TVM`, `SYM`, `GTR`<br> **Protein data***: `Blosum62`, `cpREV`, `Dayhoff`, `DCMut`, `DEN`, `FLU`, `HIVb`,`HIVw`, `JTT`, `JTT-DCMut`, `LG`, `mtART`,`mtMAM`, `mtREV`, `mtZOA`, `PMB`, `rtREV`,`stmtREV`, `VT`, `WAG`, `LG4M` (implies `+G4`), `LG4X` (implies `+R4`), `PROTGTR` <br> **Binary data (0/1)**: `BIN` <br> **Morphological/multistate:** `MULTIx_MK`, `MULTIx_GTR` (where `x` = number of states, e.g.: `MULTI8_MK` for a 8-state model with equal rates) [state encoding](https://github.com/amkozlov/raxml-ng/wiki/Input-data#state-encoding--order) <br> **Unphased diploid genotypes (10 states)**: `GTJC` `GTHKY4` `GTGTR4` `GTGTR` <br> **Fixed user-defined rates**: e.g. `HKY{1.0/2.5}` or `GTR{0.5/2.0/1.0/1.2/0.1/1.0}` or `PROTGTR{rates.txt}`. The rates above define upper triangle of the substitution matrix, e.g. for `GTR` the order is `A-C`, `A-G`, `A-T`, `C-G`, `C-T`, `G-T`|
| Stationary frequencies | `+F` or `+FC` (empirical)<br> `+FO` (ML estimate)<br> `+FE` (equal) <br>`+FU{f1/f2/../fn}` (user-defined: `f1 f2 ... fn`) <br>`+FU{freqs.txt}` (user-defined from file) |
| Proportion of <br> invariant sites | `+I` or `+IO` (ML estimate)<br>`+IC` (empirical)<br> `+IU{p}` (user-defined: `p`)
| Among-site rate <br> heterogeneity model | `+G` (discrete GAMMA with 4 categories, *mean* category rates, ML estimate of alpha) <br>`+GA` (as above, but with *median* category rates) <br>`+Gn` (discrete GAMMA with `n` categories, ML estimate of alpha) <br>`+Gn{a}` (discrete GAMMA with `n` categories and user-defined alpha `a`) <br>`+Rn` (FreeRate with `n` categories, ML estimate of rates and weights) <br>`+Rn{r1/r2/../rn}{w1/w2/../wn}` (FreeRate with `n` categories, user-defined rates `r1 r2 ... rn` and weights `w1 w2 ... wn`)|
| Ascertainment bias <br> correction | `+ASC_LEWIS` (Lewis' method)<br>`+ASC_FELS{w}` (Felsenstein's method with total number of invariable sites `w`)<br> `+ASC_STAM{w1/w2/../wn}` (Stamatakis' method with per-state invariable site numbers `w1 w2 ... wn`)
| Custom <br> character-to-state mapping | `+M{statechars}{gapchars}` e.g. `MULTI6_GTR+M{ABCDEF}{X-?}`<br>`+Mi{statechars}{gapchars}` same as above, but `statechars` are case-insensitive<br> `+M{charmap.txt}` mapping defined in `charmap.txt` file [(see below)](https://github.com/amkozlov/raxml-ng/wiki/Input-data#user-defined-state-encoding)


\* see [libpll wiki](https://github.com/xflouris/libpll/wiki/Substitution-Models) for details & references

### Multiple models

Multiple models can be defined in a RAxML-style partition file. Example:

```
JC+G, p1 = 1-100, 252-400
HKY+F, p2 = 101-180, 251
GTR+I, p3 = 181-250
```
Here, each line defines a partition and consist of three elements: 
- model specification (see above)
- partition name
- range of alignment columns

### Branch length linkage

In case of partitioned analysis, three branch length estimation modes are available:

|     Command            |   Meaning         |
|------------------------|--------------------|
| `--brlen linked`       | Branch lengths are identical for all partitions |
| `--brlen scaled`       | (**default**) Joint branch length estimation with individual per-partition scalers (i.e., branch lengths are proportional) |
| `--brlen unlinked`     | Branch lengths are estimated independently for each partition (cf. RAxML `-M` option)|

## State encoding & order

### Defaults
|Data type| Order |
|---------|-------|
|DNA      | `A C G T` |
|PROTEIN  | `A R N D C Q E G H I L K M F P S T W Y V` |
|MULTISTATE | `0 1 2 3 4 5 6 7 8 9 A B C D E F G H I J K L M N O P Q R S T U V W X Y Z ! " # $ % & ' ( ) * + , / : ; < = > @ [ \ ] ^ _ { \| } ~ ` |
|GENOTYPE (diploid unphased) | `A C G T M R W S Y K` <br> (Meaning: `A/A C/C G/G T/T A/C A/G A/T C/G C/T G/T`) |