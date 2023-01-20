# Lab 1 - Unix and Multiple Sequence Alignment

In this lab we will review some basic

## Before the class:

#### 1) Learn/review some basic Unix commands before the class.  
- If you are new to Unix, go through tutorials one and two [here](http://www.ee.surrey.ac.uk/Teaching/Unix/). Note, that you can run unix in your browser! (e.g., [here](https://www.tutorialspoint.com/unix_terminal_online.php))
- It would be very useful to know basics of the `vi(m)` editor.
I prepared a [tutorial](https://data-skills.github.io/tutorials/vi_tutorial.pdf) for you.

#### 2) Install Git/Git Bash
- On Mac: Check if Git is installed by typing `git` in your terminal. Follow the instructions if Git is not installed.
- On Windows: Download the most recent version of the program from [here](https://gitforwindows.org/).
- To learn more about git go through the following (optional) [tutorial](https://data-skills.github.io/tutorials/git.pdf)

#### 3) Get a GitHub User Account

Create a user account on [GitHub](https://github.com/join) if you don't have one already.
Be sure to choose a user ID that you are happy using for the rest of your professional career.

#### 4) Install the VPN software if you are working off campus.

Go the [link](https://iastate.service-now.com/it?id=kb_article_view&sysparm_article=KB0011105)
and follow the instructions.

## In class:

<!-- #### Connect to the ISU VPN (if working off campus)

- Launch the Cisco AnyConnect Secure Mobility Client
- Enter vpn.iastate.edu and click Connect
- Set the Group to 'Primary', login through Okta and click OK
-->

### Connect to the HPC-class server (now part of Nova)

Open the Terminal application on Mac/Linux or GitBash on Windows.
Type `ssh <ISU NetID>@nova.its.iastate.edu`, where netID is your university username.

**Imporant:** Accounts on Nova Cluster require the use of Google Authenticator. The Google Authenticator provides a six digit one-time password users must provide in addition to their username and password to log into Nova Cluster.

If you don't have Google Authenticator installed, follow the [instructions on the HPC Nova website](https://www.hpc.iastate.edu/guides/nova/access-and-login).

At the first attempt to login to Nova a GA account will be created for the user, and the email with the instructions will be sent to <ISU NetID>@iastate.edu.

### Git SetUp on Nova  
#### Linking your Nova account to GitHub

> We need to do a few things in your home directory.
> Just follow the instructions and don't worry about the details at the moment.

In your home directory, type `ssh-keygen` and press enter to confirm the name of the file.
If you get a message that the file already exist, don't overwrite it.

Type `cat ~/.ssh/id_rsa.pub` and copy your public ssh key.
Go to your [GitHub account](www.github.com) and click on your picture in the upper right corner. Select "Settings".
Choose "SSH and GPG keys" under "Personal settings". If you don't have it already, enter a new SSH key for hpc-class.
Paste your public ssh key there. Click on "Add your SSH key.

#### A few configuration steps

Because Git is meant to help with collaborative editing of files,
you need to tell Git who you are and what your email address is.
To do this, use:
`git config --global user.name "Sewall Wright"`   
`git config --global user.email "swright@adaptivelandscape.org"`  
Make sure to use your own name and email, or course!

Another useful Git setting to enable now is terminal colors:
`git config --global color.ui true`

#### Cloning a repository

Go to the [EEOB563-Spring2023 repository](https://github.com/ISU-MolPhyl/EEOB563-Spring2023) and copy its SSH address under `Clone or Download.`

Run the following command in your home directory on HPC-class:  
`git clone <repository address>`

#### Updating a repository

To update a Git repository, enter the following command:  
`git pull`


### UNIX

[Unix exercise](https://data-skills.github.io/tutorials/UNIX.html)

### Multiple Sequence Alignment

[MSA exercise](msa.pdf)

> ### A useful trick
>
> It is rather tedious to type the whole `ssh <netID>@hpc-class.its.iastate.edu` command
> and to enter the password every time you connect to HPC-class.  So here is a trick for you!
> On your own laptop computer create an .ssh directory by typing `ssh-keygen` in your home directory.
> Use the following command to paste info into the config file (which may not yet exist) in .ssh directory:
>
> ```
> echo "host hpc-class
> HostName hpc-class.its.iastate.edu
> User dlavrov" >> ~/.ssh/config
> ```
> Now enter the following command: `ssh-copy-id -i ~/.ssh/id_rsa.pub <your_username>@hpc-class.its.iastate.edu`.
> It will ask you for your hpc-class password.
>
> Next time you connect to HPC-class, just enter `ssh hpc-class`.  You won't need either to type anything else or to enter your password!
> Enjoy!
