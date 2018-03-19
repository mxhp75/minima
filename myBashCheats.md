---
layout: page
title: myBashCheats
---

This page is intended as a cheat sheet for utilities in common use in the Mac terminal.

For detailed instructions on usage always turn to the `man` page.

# A

# B

**Background**

In the Unix shell, run a program in the background by appending an `&` (ampersand) to the command:

  ```
    $ program1 input.txt > results.txt &
 
   [1] 12345 
  ```
   
> nb: we use the `>` to **redirect** the output to a file.

Running the above line of code will return this *process ID* (PID) from the shell rather than any progress we would otherwise see printed to the terminal.

-> We can use the ID to check on the status of our job by running:
 ```
   $ jobs
 
  [1] + Running program1 input.txt > results.txt 
 ```
 
 We can see that our job is number [1]. This is important if we want to return to see how the job is running.
 
 -> Use `$ fg` to bring the most recent process to the foreground.
 
 -> Use `$ job %1` to find the job number of the first process running.
 
 -> Use `$ fg %<num>` where `<num>` is the job ID (not the process ID).
 
 -> If you have a job running in the foreground (fg) and you want to get on with something else, suspend the current job with `Control-z`, then send to the back ground using `bg`.
 
 ```
  $ program1 input.txt > results.txt    # woops - forgot to append the & to run on the background
  $ Control-z                           # suspend the current job running in the foreground
  $ bg                                  # send the suspended job to the background
  ```
  
 > nb: also see **screen** if you want to be able to exit the shell and keep the job running (although I need to check if this is only for VM).

**Brace Expansion**

We can reduce our keystrokes by getting the terminal to do some work for us. Say for example that you wanted to say hello to 3 friends, but didn't want to type out "hello" three times.

  ```
   $ echo Hello-{John, Paul, Ringo}

  Hello-John Hello-Paul Hello-Ringo
  ```  
> nb: Bash uses the `echo` command to print to the terminal
  
**Using Brace Expansion to make a Project Directory**

Saying Hi to friends might not come up that often, but creating project (and other) directories does. Using the brace expansion here means we don't need to type out the `mkdir` command a bunch of times and helps to keep our directory structure nice and neat.
  
  ```
    $ mkdir -p projectDirectory/{data/sequences, scripts, trimmed}
  ```
  
   * /projectDirectory
   * /projectDirectory/data/sequences
   * /projectDirectory/scripts
   * /projectDirectory/trimmed
      
> nb: using -p after `mkdir` tells Bash to make any directories along the way if they don't already exist.  

# C

**Change Directry**

Moving between directories is quite easy on the command line if you keep your directory structure in mind.

You can treat your directory structure like a series of nested trees or walkways that you can move up and down through, or you can move around using an **absolute path**

The main command when changing directories is `cd`, quite literally "**c**hange **d**irectory"

```
  $ cd ../
```

will move you "up" one directory.

**Concatenate**

The `cat` utility in the terminal will read files in sequence, and write them to screen (as standard out) eg.

```
  $ cat my_file.txt
```

will print my text file to the screen. 

We can also use the `cat` utility to redirect a file to a new file as output

```
  $ cat my_original_file.txt > my_new_file.txt
```
or to concatenate multiple files into a single file

```
  $ cat my_first_file.txt my_second_file.txt > my_new_file.txt
```
> nb: using `>` will redirect the input file(s) to a new output file, overwriting contents if the file already exists. Use `>>` if you want to append to an existing file rather than overwrite it.

The `cat` utility can also be used in more complex ways such as combining multiple files. See my blog post on concatenating fastq files from multiple lanes into single files using a `while read` loop for details.
  
**Conda virtual environment**

To create a new conda virtual environment

```
  $ conda create -n yourNewEnvironmentName
```
> nb: you can add the packages you want to be inside your virtual environment in this step, and specify the version of package you want eg ` $ conda create -n youreNewEnvironmentName python=2.7`

To delete a virtual environment

```
  $conda remove -n yourEnvironmentName -all
```
In the interest of reproducible research, it's a good idea to include the details of your virtual environment with any project repo. Conda provides a simple way to this by including a project.yaml.

```
  $ conda env export > my_environment.yaml
```

This .yaml file will include all the information conda needs to recreate your virtual environment including all of tha packages and their version.

> nb: create a replica virtual environment using `conda create -f my_environment.yaml`

To see a list of your conda virtual environments use

```
  $ conda info -e
```
or
```
  $ conda env list
```

To see a list of tools in your existing conda environment use

```
  $ conda list
```

To use your conda virtual environment
  1. `$ module load Anaconda3`
  2. `$ source activate myEnvironmentName`
and to deactivate once you're finished for the day
  3. `$ source deactivate myEnvironmentName`
  
For a great conda cheat sheet ![Conda Cheat](/conda-cheatsheet.pdf)

**Copy**

Making a copy of a file from the command line is as easy as `cp <source> <destination>` eg.

```
  $ cp my_file.txt path/to/new_file_name.txt
```

> nb: if you are copying a file from a different directory you need to include the full or relative path 
`cp /path/to/original_file.txt /path/to/new_file_name.txt`

>    you can use `-i` to make the process interactive, or `-v` to make the process "verbose" (print what's happening to the screen)


**Count file in a Directory**

It's surprising how many times you need to just count the files you have in a directory

```
  $ ls | wc -l
```

will return the number of files there are in the directory you are currently in.

> nb: this will also work if you use `ll | wc -l` or `ls -l | wc -l` but be careful as both of these options have a header and will increas the count by 1.

**Cut**

The `cut` utility has a good man page, this is what I use to cut culumns 1, 7, and everything after 7 from the feature counts output file.

```
  $ cut -f 1,7- source.txt > just_counts.txt      # -f selects only fields - here that acts like columns in a spreadsheet
```

# D

**Divert**

Diverting output between programmes can be a good way of saving intermediate files you may want (or need) to look at later for things like quality checking and debugging.

To divert standard output to a temporary file while also sending to standard out (and therefore to another utility or program if that's what you want) you can use `tee`.

```
  $ program1 input.txt | tee intermediate_file.txt | program2 > results.txt
```

# E

**Echo**

`Echo` is used in the terminal to print output to the screen. Often `$ echo Hello World` is the very first command people will use in the terminal. There are many other uses for `echo`, for example if I type `echo $0` the terminal will return `-bash`, which is the shell I use.

**Exit Status**

You can find the exit status of the previous program run by using

```
  $ echo $?
```
> nb: `$?` is where the Unix shell puts the exit message after you run a command on the command line.

An exit status of 
  - `0` = process ran successfully
  - `!0` = some sort of error occured
  
-> Use `&&` if you want the next command to continue only if the previous process was successful
-> Use `||` if you want the next command to continue only if the previoud process was un-successful
-> Combine these "only if successful" and "only if not successful" options on the command line.

```
  $ program1 input.txt > intermediate_results.txt && \
    program2 intermediate_results.txt > final_results.txt
```

Here `input.txt` is fed into `program1` and the output from `program1` is redirected to `intermediate_results.txt`. From here, because we have used `&&`, this intermediate file will only be fed into `program2` if the first process completed successfully.

> nb: You can also use a **;** (semicolon) for multiple commands with no care for the exit status.
``` 
  $ cd ../; ls            # change directory up one, and then list.
```

# F

# G

# H

# I

# J

# K

# L

# M

**Merge**

```
#!/bin/bash

while read line
        do
                L1=$(echo "$line" | cut -f 1)
                L2=$(echo "$line" | cut -f 2)
                L3=$(echo "$line" | cut -f 3)
                L4=$(echo "$line" | cut -f 4)
                MERGE=$(echo "$line" | cut -f 5)
                cat ${L1} ${L2} ${L3} ${L4} > /path/to_my/mergeFiles/${MERGE}
        done < /path/to_my-input.txt
```

> nb: my_input.txt is in the format:
  ``` 
  path/to_file1_lane1,path/to_file1_lane2,path/to_file1_lane3,path/to_file1_lane4,new_file1_name
  path/to_file2_lane1,path/to_file2_lane2,path/to_file2_lane3,path/to_file2_lane4,new_file1_name
  ```
  

# N

# O

# P

**Permissions**

Use `chmod` to change the permissions on a file (eg to read only, read write etc).

```
  $ chmod u+x myscript.sh         # The "u" makes this change user specific
```

> nb: use `ls -l` to see the permission a file currently has (this will list files in the current directory)
>     Not having the correct permission is a common reason for a script not to run.

# Q

# R

# S

# T

# U

# V

# W

# X

# Y

# Z
