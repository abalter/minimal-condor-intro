# Introduction to Creating and Running Programs

## hello.py

Run a simple python program. Don't worry if you don't know python. But you 
should be familiar with the concept of running a script in some language like 
bash or R etc.

See the code [here](http://gitlab.bcore.ohsu.edu/ohsu/simple-condor-intro/blob/master/hello.py).

1. Run it

    python hello.py
    
1. Make executable so you can run it without saying `python`

    chmod 755 hello.py
    
    ./hello.py

1. Uncomment error 

    ./hello.py
    
  You will see that it threw an error. Now run it so that the output and error 
  go to a file, rather than the console (also known as stdout).

1. Redirect stdout and stderr

    ./hello.py 1>out.txt 2>err.txt
    
1. Display the files. `cat` is one way to spit the content of a file to the console.
    
    cat out.txt
    
    cat err.txt
    
## sleepytime.sh

This is a simple program with a delay. We are doing this so that later when you 
submit it to condor, it won't finish right away, and you will be able to see it 
in the queue. Code [here](http://gitlab.bcore.ohsu.edu/ohsu/simple-condor-intro/blob/master/sleepytime.sh).

`sleepytime.sh` is in a programming language known as shell scripting (which has 
an assortment of flavors). Shell scripting is the basic toolkit for people who 
use linux operating systems, and to an extent MacOS as well. This is also a very 
common language for running bioinformatics pipelines.

The important difference with this script is that the executable `sleepytime.sh` 
takes an _argument_ which is a piece of information the script needs to run. If 
you are not familiar with bash scripting, you can google to find out more.

1. Run it

    bash sleepytime.sh 1
    
    bash sleepytime.sh 5
    
1. Make exectutable

    chmod 755 sleepytime.sh
    
    ./sleepytime.sh 1
    
    ./sleepytime.sh 5
    
1. Uncomment error

    ./sleepytime.sh 1
    
1. Redirect stdout and stderr

    ./sleepytime.sh 2 1>out.txt 2>err.txt
    
    less out.txt
    
    less err.txt
    
`less` is another way to spit the output of a file to the console. Google it to 
learn how to use it.
    
# Submitting Jobs to Condor

## hello.sub

1. Submit `hello.sub`

  This submit file (code [here](hello.sub)) is a minimal condor submit script 
  that will log the process. Try it with the error commented out and not 
  commented out.`queue 100` means submit it 100 times. 

    condor_submit hello.sub

1. Quickly check the queue

    condor_q
    
1. Check the log files

1. Repeat with/without the error

## sleepytime.sub

This example (code [here](sleepytime.sub) demonstrates submitting an executable that takes an argument.

1. Submit `sleepytime.sub`

    condor_submit sleepytime.sub

1. Check the queue

    condor_q
    
1. Read the log files.


## Resource:

https://swc-osg-workshop.github.io/2016-01-06-UNL/novice/DHTC/04-HTCondor-Submitting.html