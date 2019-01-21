# Lab 1 - Unix, Git and GitHub, SSH

This lab teaches about/reviews three important systems that we'll be using through the semester.

## Prerequisites:

#### 1) Learn/review some basic Unix commands before the class.  
If you are new to Unix, go through tutorials one and two [here](http://www.ee.surrey.ac.uk/Teaching/Unix/). Note, that you can run unix in your browser! (e.g., [here](https://www.tutorialspoint.com/unix_terminal_online.php)) 

#### 2) Install GitBash if you are a Windows user.
Download the most recent version of the program from [here](https://gitforwindows.org/).

#### 3) Get a GitHub User Account

Create a user account on [GitHub](https://github.com/join) if you don't have one already. Be sure to choose a user ID that you are happy using for the rest of your professional career.

## Connecting to the HPC-class server

Open the Terminal application on Mac/Linux or GitBash on Windows. 
Type `ssh <netID>@hpc-class.its.iastate.edu`, where netID is your university username. It will ask you for a password. Use your university password to enter your account.

We will do a few things in your home directory. Just follow the instructions and don't worry about the details at the moment.

## Basic Git

#### Git SetUp

Because Git is meant to help with collaborative editing of files, 
you need to tell Git who you are and what your email address is. 
To do this, use:
`git config --global user.name "Sewall Wright"`   
`git config --global user.email "swright@adaptivelandscape.org"`  
Make sure to use your own name and email, or course!

Another useful Git setting to enable now is terminal colors:
git config --global color.ui true

#### Cloning a repository

Go to the EEOB563-Spring2019 repository and copy its HTTPS address under `Clone or Download.`

Run the following command in your home directory on HPC-class:  
`git clone <repository address>`

#### Updating a repository

To update a Git reposity, enter the following command:  
`git pull`


## Lab tutorial

Lab 1: [Unix, Git, SSH](Unix.md)

## Additional tutorials

[Git/GitHub](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab1/git.pdf)  
[VI](https://isu-molphyl.github.io/EEOB563-Spring2018/computer_labs/lab1/vi_tutorial.pdf)  



