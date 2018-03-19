# A

# B

**Background**

In the Unix shell, run a program in the background by appending an `&` (ampersand) to the command:

  ```
    $ program1 input.txt > results.txt &
  
  ```
   [1] 12345 
   
> nd: we use the `>` to **redirect** the output to a file.

Running the above line of code will return this *process ID* (PID) from the shell rather than any progress we would otherwise see printed to the terminal.

:arrow_right: We can use the ID to check on the status of our job by running:
  ```
   $ jobs
  ```
   [1] + Running program1 input.txt > results.txt 
 
 We can see that our job is number [1]. This is important if we want to return to see how the job is running.
 
 :arrow_right: Use `$ fg` to bring the most recent process to the foreground.
 
 :arrow_right: Use `$ job %1` to find the job number of the first process running.
 
 :arrow_right: Use `$ fg %<num>` where `<num>` is the job ID (not the process ID).
 
 :arrow_right: If you have a job running in the foreground (fg) and you want to get on with something else, suspend the current job with `Control-z`, then send to the back ground using `bg`.
 
 ```
  $ program1 input.txt > results.txt    # forgot to append the &
  $ Control-z
  $ bg 
  ```
  
 > nd: also see **screen** if you want to be able to exit the shell and keep the job running (although I need to check if this is only for VM).

**Brace Expansion**

We can reduce our keystrokes by getting the terminal to do some work for us. Say for example that you wanted to say hello to 3 friends, but didn't want to type our "hello" three times.

  ```
   $ echo Hello-{Mike, Julia, Helen}
  ```
  
  Hello-Mike Hello-Julia Hello-Helen
  
> nb: Bash uses the `echo` command to print to the terminal
  
**Using Brace Expansion to make a Project Directory**

Saying Hi to friends might bot come up that often, but creating project (and other) directories does. Using the brace expansion here means we don't need to type out the `mkdir` command a bunch of times and helps to keep our directory structure nice and neat.
  
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
