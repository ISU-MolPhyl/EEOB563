# Lab #2 Multiple Sequence Alignment and Parsimony analysis

The objective of this lab is to learn how to do a parsimony analysis using **PAUP** and **TNT**. 
We will also review how to align molecular sequences with **MAFFT**.

## First things first

### Modifying the PATH Variable
The PATH environment variable is a colon-delimited list of directories 
that your shell searches through when you enter a command. Your path 
tells the Unix shell where to look on the system when you request a 
particular program. To find out what your path is, at the Unix shell 
prompt, enter: `echo $PATH`. I have installed PAUP and TNT in a shared 
directory for the class (/shared/class/eeob563). While you can run these 
programs by using the full path name: `/shared/class/eeob563/paup`, it's 
easer to add this directory to the path:

1. Add `/shared/class/eeob563` directory to your path:
	* Log in to HPC class using `ssh <netID>@hpc-class.its.iastate.edu` command.  
	* Open your bash profile file in vi: `vi ~/.bash_profile`;
	* Go to the `PATH=...` line using the down arrow;  
	* type `A` (for add) and add the following text to the end of the line: `:/shared/class/eeob563`
	* press `ESC`
	* type `ZZ` (or `:wq`) to save and quit the file;
2. Run `source ~/.bashrc`; <!-- can use `exec bash` instead -->
3. Type `paup` to make sure that you can run the program;
4. Type `q` to quit PAUP.

### Updating the class repository

We also need to update the class repository (`cd EEOB563-Spring2021; git pull`) and go to the `computer_labs/lab2` directory.

## Mafft

[**MAFFT**](https://mafft.cbrc.jp/alignment/software/) (for Multiple Alignment using Fast Fourier Transform) 
is a multiple sequence alignment program for unix-like operating systems. The first version of MAFFT 
used an algorithm based on progressive alignment, in which the sequences were clustered with the help of the Fast Fourier Transform (hence the name).

### mafft on HPC-class
MAFFT is already installed on HPC class as one of the modules. You can load it with `module load mafft`. 
(To see all the version of mafft in modules use `module -r spider "mafft"`

### mafft --auto

The simplest way to run mafft is by using the `--auto` option:  
`mafft --auto <filename.fa> > <alignment.fa>`, where `filename.fa` is the name of a file of molecular 
sequences in FASTA format and `alignment.fa` is the name of the output file.

### Additional useful options
#### Input

* `--nuc` Assume the sequences are nucleotide. Default: auto
* `--amino` Assume the sequences are amino acid. Default: auto

#### Output

* `--clustalout` and `--phylipout` Output format: clustal format. Default: off (fasta format)  
* `--inputorder` Output order: same as input. Default: on
* `--reorder` Output order: aligned. Default: off (inputorder)
* `--treeout`Guide tree is output to the input.tree file. Default: off

#### Direction of nucleotide sequences
Two options generate reverse complement sequences, as necessary, and align them together with the remaining sequences.  
`mafft --adjustdirection input > output` is based on 6 mer counting and faster;  
`mafft --adjustdirectionaccurately input > output` is based on DP and slower.

## DATA
1. We will use a set of cytochorome b aa sequences for this exercise. The sequences are 
in the `computer_labs/lab2` directory of the class repository. If you still have problems with the GitHub, you can 
download sequences directly into your directory using the following unix command:
`wget https://raw.githubusercontent.com/ISU-MolPhyl/EEOB563-Spring2021/master/computer_labs/lab2/cob_aa.fasta` 
2. Align these sequences using mafft and save them in fasta format.
3. To use this alignment in PAUP, we'll need to convert it into the Nexus format.
4. Read brief Wikipedia descriptions of [FASTA](https://en.wikipedia.org/wiki/FASTA_format) 
and [Nexus](https://en.wikipedia.org/wiki/Nexus_file) file formats.

## PAUP

[PAUP tutorial](./PAUP.md)

## TNT (optional)

[TNT tutorial](./TNT.md) If you like a challenge you can try TNT with the dinosaurs [data](dino.txt)


