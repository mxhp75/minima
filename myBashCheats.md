---
layout: page
title: myBashCheats
---

This page is intended as a cheat sheet for utilities in common use in the Mac terminal.

For detailed instructions on use always turn to the `man` page.

# A

# B

**Background**

In the Unix shell, run a program in the background by appending an `&` (ampersand) to the command:

  ```
    $ program1 input.txt > results.txt &
  
  ```
   [1] 12345 
   
> nb: we use the `>` to *redirect* the output to a file.

Running the above line of code will return this *process ID* (PID) from the shell rather than any progress we would otherwise see printed to the terminal.

-> We can use the ID to check on the status of our job by running:
  ```
   $ jobs
  ```
   [1] + Running program1 input.txt > results.txt 
 
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
   $ echo Hello-{Mike, Julia, Helen}
  ```
  
  Hello-Michelle Hello-Julia Hello-Helen
  
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

# D

# E

# F

# G

# H

# I

# J

# K

# L

# M

# N

# O

# P

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
