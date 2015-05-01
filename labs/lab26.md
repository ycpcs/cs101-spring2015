---
layout: default
title: "Lab 26: Baby Names"
---

# Getting Started

As always, you may refer to [Lab 1](lab01.html) if you need a reminder about how to start the **Cygwin Bash Shell** or **Notepad++**.

Begin by downloading [CS101\_Lab26.zip](CS101_Lab26.zip). Save the zip file in the **H:\\CS101** directory.

Start the **Cygwin Bash Shell** and run the following commands:

    cd h:
    cd CS101
    unzip CS101_Lab26.zip
    cd CS101_Lab26

Start the **Notepad++** text editor. Use it to open the file

> **H:\\CS101\\CS101\_Lab26\\BabyNames.cpp**

When you are ready to compile the program, in the Cygwin window type the command

    make

To run the program, in the Cygwin window type the command

    ./BabyNames.exe

### Your task

In this lab, you will write a program to perform queries on a file containing [baby name popularity data](http://www.ssa.gov/OACT/babynames/) from the Social Security Administration.

This is the input file that your program will use:

> [babynames.txt](babynames.txt)

Save it in the directory containing your lab files (`CS101_Lab26`).

The program should prompt the user to enter a filename, a name, a gender (M for male or F for female), and a decade (1900, 1910, etc.)  The program should then read the contents of the baby name data file looking for a matching record.  If a matching record is found, it should print the popularity rank of the specified name in the specified decade.

Here is an example run of the program (user input in **bold**):

<pre>
Input file: <b>babynames.txt</b>
Name? <b>Hubert</b>
Male (M) or Female (F): <b>M</b>
Decade? <b>1900</b>
In the 1900s, the name Hubert was ranked 122
</pre>

Another run:

<pre>
Input file: <b>babynames.txt</b>
Name? <b>Harriet</b>
Male (M) or Female (F): <b>F</b>
Decade? <b>1940</b>
In the 1940s, the name Harriet was ranked 183
</pre>

One more:

<pre>
Input file: <b>babynames.txt</b>
Name? <b>Cadwalader</b>
Male (M) or Female (F): <b>M</b>
Decade? <b>1900</b>
I did not find the name Cadwalader in the 1900s
</pre>

## Hints

Each line of the file represents the popularity of a particular name (male or female) in a particular decade of the 20th century.  (Here is the first line of the file:

    1900 1 M John 84602

This line indicates that John was ranked number 1 for male baby names in the 1900s.  (The last field is the number of babies recorded as named John in the 1900s.)

You can read an entire line of input from the file as follows:

{% highlight cpp %}
int decade, rank, count;
char gender;
char name[200];

...

if (fscanf(in, "%i %i %c %s %i", &decade, &rank, &gender, name, &count) == 5) {
    // one line from the file was read successfully
    ...
}
{% endhighlight %}

This assumes `in` is a variable containing the file handle of the file you're reading from.

You can stop reading lines from the file when a matching record is found, or when the call `fscanf` indicates that a record was not read successfully.

# Submitting

When you are done, run the following command from the Cygwin bash shell:

    make submit

You will be prompted for your Marmoset username and password, which you should have received by email. Note that your password will not appear on the screen.

**Important**:

> You **must** submit your work before leaving class. If you do not submit work, you will not receive any credit for the lab.

<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->
