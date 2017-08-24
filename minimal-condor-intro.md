# A Very Minimal Introduction to Creating and Running Programs and Submitting Them as Jobs to HTCondor

**NOTE:** In order to do these exercises, you need:
* Access to a cluster using the HTCondor scheduler. If you don't have that, you are probably not
looking at this anyway.
* A program that connects you to a command line on that cluster. Ditto above.
* The ability to use a command line editor. This means you don't open a separate program
such as MS Word to create or edit files. You use a program that works right in your terminal
console. If you don't already know how to do this, you will need to do a bit of learning. I suggest
looking at 
    - https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/
  and
    - https://www.tecmint.com/linux-command-line-editors/
  
Also, if you are a command line novice, I strongly suggest the following:
  *  https://www.codecademy.com/learn/learn-the-command-line
  and perhaps
  * http://www.vikingcodeschool.com/web-development-basics/a-command-line-crash-course
  and
  * https://www.codeschool.com/screencasts/unix-basics-part-1

## Task: Run a simple python program from the command line. 
Don't worry if you don't know python. This exercise is just to make sure you know how
to run a script or program from the command line. The method is the same whether the 
program is written in a language such as shell (sh), R, Perl, etc.

In the _code_ directory you will find the file _hello.py_.

1. Look at the file

    cat hello.py

1. Run it

    python hello.py
    
1. Make the script an _executable_ so you can run it without saying `python`

    chmod 755 hello.py
    
    ./hello.py

1. Uncomment error (line #8, see instructions in the file)

    ./hello.py
    
  You will see that it threw an error. Now run it so that the output and error 
  go to a file, rather than the console (also known as stdout).

1. Redirect stdout and stderr

    ./hello.py 1>out.txt 2>err.txt
    
1. Display the files. `cat` is one way to spit the content of a file to the console.
    
    cat out.txt
    
    cat err.txt
    
## Task: Run a program that takes an argument
In the code directory you will find _sleepytime.sh_. This is a simple program with a delay. 
We are doing this so that later when you submit it to condor, it won't finish right away, 
and you will be able to see it in the queue.

`sleepytime.sh` is written in a programming language known as _shell scripting_ (which has 
an assortment of flavors). Shell scripting is the basic toolkit for people who 
use linux operating systems, and to an extent MacOS as well. This is also a very 
common language for running bioinformatics pipelines.

The important difference with this script and _hello.py_ is that the executable `sleepytime.sh` 
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
    
## Task: Submit a Job to Condor

1. Submit `hello.sub` (in the _code_ directory) to Condor

  This submit file is a minimal condor submit script that will log the process. 
  Try it with the error commented out and not commented out.`queue 10` means submit 
  it 10 times.

    condor_submit hello.sub

1. Quickly check the queue

    condor_q
    
1. Check the log files using `cat` or `less`

1. Repeat with/without the error

## Task: Submit a Job with Arguments

This example demonstrates submitting an executable that takes an argument. Notice
that here we have multiple `queue` lines, each with a different argument.

1. Submit _sleepytime.sub_

    condor_submit sleepytime.sub

1. Check the queue

    condor_q
   
  You can continue to monitor the queue and watch the files complete one at a time.
  The files with the shortest sleep times may finish first, but it will depend on the
  order in which the HTCondor scheduler actually sends the job to compute nodes. You can
  give Condor additional information such as memory needed, CPU specs needed, time needed,
  etc. that help it job out the tasks more efficiently.
    
1. Read the log files.


## Resource:

https://swc-osg-workshop.github.io/2016-01-06-UNL/novice/DHTC/04-HTCondor-Submitting.html
