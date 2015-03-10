---
layout: default
title: "Assignment 3: Take Me Out To The Ballgame"
---

*Update 3/10* &mdash; The **Hints** section has been updated with information about computing the standard deviation

**Due**: Friday, March 13th by 11:59 PM

Primary course learning outcomes supported by this assignment:

- Understand and use arrays
- Understand and apply control structures such as conditional and loops

# Getting Started

Start by downloading [CS101\_Assign03.zip](CS101_Assign03.zip), saving it in the CS101 directory within your home directory.

Start a Cygwin Bash Shell (or Linux terminal, or MacOS terminal) and run the following commands:

    cd h:
    cd CS101
    unzip CS101_Assign03.zip
    cd CS101_Assign03

(Note that you should omit the cd h: step on Linux and MacOS.)

Using a text editor (e.g., Notepad++), open the file 

    CS101/CS101_Assign03/Statistics.cpp

You will add your code to this file.

# Your Task

Major League Baseball (MLB) season starts on 5 April this year.   Along with the hot dogs and popcorn, there will be hits, strikes, and homeruns.  Included with this great national tradition is the collection of player and team statistics.  Over the years, many people have developed databases to capture these numbers, e.g.  Sean Lahman (see http://www.seanlahman.com/baseball-archive/statistics/).

Declare an array that will hold the batting averages (values between 0 and 1000) of a given year. From this set, calculate the mean, median, and standard deviation.  We provide a function that sorts that array for the median calculation.  Finally, output a histogram using the following guidelines:

* Separate batting averages into the following 10 groupings:

        001-100 
        101-200 
        201-300
        301-400 
        401-500 
        501-600 
        601-700
        701-800 
        801-900 
        901-1000

* For each of the groupings, count the number of batting averages that fall into that range.  Print an asterisk "\*" for every 10 entries.  For example, if there are 115 entries for batting averages that fall in the range 201 and 300, there would be 11 asterisks printed out. 

The following files are in the **CS101\_Assign03** directory:

* **Makefile**  &mdash; to compile our file
* **submitToMarmoset.pl** &mdash; used to submit your assignment to the Marmoset server
* **Utils.cpp** &mdash; this file contains functions that you will use in **Statistics.cpp**.  It includes the following functions.

  * `int getFileSize(char fileName[])` &mdash; given a file name (as a string) , this function will return the number of lines in that file.
  * `void  initializeArray( int list[], int size)` &mdash; given an integer array and its size, this function initializes the given array to all zeroes.  
  * `void loadArray(int list[], int size, char fileName[])` &mdash; given an integer array, it’s size, and a file name as a string, this function will load the batting averages from the given file into the given array.
  * `void sortArray(int list[], int size)` &mdash; given an integer array and its size, this function sorts the array in ascending order.

* 2014.txt &mdash; data file with batting averages for all MLB players for the 2014 season.
* 2005.txt &mdash; data file with batting averages for all MLB players for the 2005 season.

**Calling a function:** There are hints in the `Statistics.cpp` file to help you with calling the functions located in the `Utils.cpp` file.  Please refer to pp. 119 &mdash; 130 in the text for more details on functions.

The following is the sample output when the “2005.txt” file is used.

    Array size:             988
    Mean:                   203.03
    Standard deviation:     132.17
    Median:                 238
      averages      qty
     ----------     ---
    [001 -  100]     42: ****
    [101 -  200]    169: ****************
    [201 -  300]    482: ************************************************
    [301 -  400]     94: *********
    [401 -  500]     16: *
    [501 -  600]      0:
    [601 -  700]      2:
    [701 -  800]      1:
    [801 -  900]      0:
    [901 - 1000]      6:

## Grading

50% level - program compiles

60% level - properly declare and load arrays

70% level - properly calculate and output the mean, median, and standard deviation

80% level - properly calculate and output the histogram

90% level - proper coding style

## Hints

* Declare an integer array to hold each batting averages (this is provided to you).
* Declare a second integer array with 10 elements to store the counts of batting averages to be used for the histogram. 
* Use the provided functions in **Utils.cpp**.  But do not modify this file!
* See <http://www.mathsisfun.com/data/standard-deviation.html> for an explanation of how to compute the standard deviation

# Submitting

To submit your work, make sure your **Statistics.cpp** file is saved, and in the Cygwin window type the command

    make submit

Enter your Marmoset username and password (which you should have received by email.) Note that your password will not be echoed to the screen. Make sure that after you enter your username and password, you see a message indicating that the submission was successful.

If the **make submit** command does not work, you can [submit using the web interface](../submitting.html) (see the link for details).

**Important**: Make sure that you check the file(s) you submitted to ensure that they are correct. Log into the server using the following URL (also linked off the course homepage):

> <https://cs.ycp.edu/marmoset/>

You should see a list of labs and assignments. In the row for **assign03**, click the link labeled **view**. You will see a list of your submissions. Download the most recent one (which should be listed first). Verify that it contains the correct files.

**You are responsible for making sure that your submission contains the correct file(s).**

<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->
