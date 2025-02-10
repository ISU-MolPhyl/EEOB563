# Lab #2 Parsimony analysis with PAUP and TNT

The objective of this lab is to learn how to do a parsimony analysis using **PAUP** and **TNT**.
We will also review how to align molecular sequences with **MAFFT**.

## First things first

### Modifying the PATH Variable
The PATH environment variable is a colon-delimited list of directories that your shell searches through when you enter a command. 
Your path tells the Unix shell where to look on the system when you request a particular program. 
To find out what your path is, at the Unix shell prompt, enter: `echo $PATH`. 
I have installed PAUP and TNT in a shared directory for the class (/work/class-faculty/dlavrov/eeob563/bin). 
While you can run these programs by using the full path name: `/work/class-faculty/dlavrov/eeob563/bin/paup`, it's easer to add this directory to the path:

1. Add `/work/class-faculty/dlavrov/eeob563/bin` directory to your path:
	* Log in to Nova using `ssh <netID>@nova.its.iastate.edu` command.  
	* Open your bash profile file in vi: `vi ~/.bash_profile`;
	* Go to the `PATH=...` line using the down arrow;  
	* type `A` (for add) and add the following text to the end of the line: `:/work/class-faculty/dlavrov/eeob563/bin`
	* press `ESC`
	* type `ZZ` (or `:wq`) to save and quit the file;
2. Run `source ~/.bashrc`; <!-- can use `exec bash` instead -->
3. Type `paup` to make sure that you can run the program;
4. Type `q` to quit PAUP.

### Working on the HPC-class partition
When you log in to a computer cluster you enter the "head node". 
This node is shared with all the other users of the cluster.
To "reserve" a "private" node, use the `salloc -p instruction -N 1 -n 4 -t 15 -A s2025.eeob.563.1` command.
Running programs on this node will not interfere with the other work on the cluster.

### Working on your personal computers  
Although we will use the Nova cluster for the class exercise, you can also download PAUP from its website and work on your personal computer: [https://paup.phylosolutions.com](https://paup.phylosolutions.com/)

### Updating the class repository
We also need to update the class repository and go to the proper directory:
- `cd EEOB563-Spring2025; git pull`)  
- `cd computer_labs/lab2`.

## PAUP

[PAUP tutorial](./PAUP.md)

## TNT (optional)

[TNT tutorial](./TNT.md) If you like a challenge you can try TNT with the dinosaurs [data](dino.txt)
