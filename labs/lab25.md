---
layout: default
title: "Lab 25: Balance Sheet"
---

# Getting Started

As always, you may refer to [Lab 1](lab01.html) if you need a reminder about how to start the **Cygwin Bash Shell** or **Notepad++**.

Begin by downloading [CS101\_Lab25.zip](CS101_Lab25.zip). Save the zip file in the **H:\\CS101** directory.

Start the **Cygwin Bash Shell** and run the following commands:

    cd h:
    cd CS101
    unzip CS101_Lab25.zip
    cd CS101_Lab25

Start the **Notepad++** text editor. Use it to open the files

> **H:\\CS101\\CS101\_Lab25\\BalanceSheet.cpp**

When you are ready to compile the program, in the Cygwin window type the command

    make

To run the program, in the Cygwin window type the command

    ./BalanceSheet.exe

# Your Task

The program prompts the user to enter the name of a file.  The file consists of an integer, specifying a number of bank accounts, and a series of entries, where each entry is an account number and an amount (positive or negative.)

Here is an example input file (this is `ledger1.txt`, which is included with the lab files):

    5
    0 1000.00
    1 650.00
    2 4375.60
    3 933.15
    4 556.10
    4 3300.90
    3 -112.45
    0 6555.44
    2 33.40
    1 -197.88

This input specifies that there are 5 bank accounts, and contains 10 entries.  In each entry, the bank account number is an integer (with 0 signifying the first bank account), and a floating point value specifying the amount that should be added to or subtracted from the account balance.

When the program runs, it should start with each account balance set to 0.  Then, as the program reads each entry, it should print a message specifying how much is being added to or subtracted from the account, and update the account balance appropriately.  Once all of the entries have been read and processed, the program should print the final balance of each account.

Here is an example run of the program (user input in **bold**):
<pre>
Load which file? <b>ledger1.txt</b>
Adjust balance of account 0 by 1000.00
Adjust balance of account 1 by 650.00
Adjust balance of account 2 by 4375.60
Adjust balance of account 3 by 933.15
Adjust balance of account 4 by 556.10
Adjust balance of account 4 by 3300.90
Adjust balance of account 3 by -112.45
Adjust balance of account 0 by 6555.44
Adjust balance of account 2 by  33.40
Adjust balance of account 1 by -197.88
Final balances:
Balance  0: $  7555.44
Balance  1: $   452.12
Balance  2: $  4409.00
Balance  3: $   820.70
Balance  4: $  3857.00
</pre>

Another example run, using `ledger2.txt` as the input file (user input in **bold**):

<pre>
Load which file? <b>ledger2.txt</b>
Adjust balance of account 0 by 4600.30
Adjust balance of account 1 by 890.55
Adjust balance of account 2 by 55602.84
Adjust balance of account 0 by 100.00
Adjust balance of account 0 by 250.00
Adjust balance of account 0 by -55.00
Adjust balance of account 2 by  67.80
Adjust balance of account 1 by 1200.00
Adjust balance of account 0 by 770.20
Final balances:
Balance  0: $  5665.50
Balance  1: $  2090.55
Balance  2: $ 55670.64
</pre>

# Hints

The `filename` array will contain the name of the file the user enters.  So, your call to `fopen` should look something like:

{% highlight cpp %}
fopen(filename, "r")
{% endhighlight %}

You will need to declare a variable whose type is `FILE *` to store the handle to the open file.

Use an array of `double` values to keep track of the account balances.  There will not be more that `MAX_ACCOUNTS` number of accounts.  Don't forget to initialize each balance to zero.

Use `fscanf` to read the number of accounts and the data (account number and transaction amount) in each entry.

The `fscanf` function returns the number of values successfully read.  This gives you a way of detecting the end of the input file: if you are attempting to read an entry (which should consist of two values), and `fscanf` returns a value less than 2, you can assume that the program has reached the end of the input file.

Don't forget to use the `fclose` function to close the file after the program has read all of the input from the file.

# Submitting

When you are done, run the following command from the Cygwin bash shell:

    make submit

You will be prompted for your Marmoset username and password, which you should have received by email. Note that your password will not appear on the screen.

**Important**:

> You **must** submit your work before leaving class. If you do not submit work, you will not receive any credit for the lab.

<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->
