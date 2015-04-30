---
layout: default
title: "Lecture 20: File I/O"
---

# File I/O

In the programs we've written so far:

* all of the input has come from the keyboard (using scanf, getchar functions)
* all of the output has been sent to the console window (using the printf function)

The abstraction for both input and output is a stream of characters:

* input is a stream (sequence) of characters arriving from the keyboard
* output is a stream of characters being sent to the console window

C uses the same abstraction, streams of characters, for input from files and output to files.

## File handles, opening and closing files

Before you can read from or write to a file, you need to open the file.  To open a file, use the fopen function.

<pre>
fopen( <i>filename</i>, <i>mode</i> )
</pre>

The filename is a character string indicating the name of the file to open.

The mode is a string indicating how the file should be opened:

* for reading
* for writing
* for both reading and writing
* text or binary mode
* if writing, should the file be truncated (overwritten) or appended to

Examples of modes:

> Mode string | Meaning
> ----------- | -------
> `"r"` | open for reading text
> `"w"` | open for writing text
> `"a"` | open for writing, append to existing contents
> `"r+"` | open for both reading and writing text
> `"w+"` | open for both reading and writing text: file is created if it doesn't exist
> `"rb"` | open for reading binary data
> `"wb"` | open for writing binary data

We won't be discussing binary I/O.

The result (return value) of calling the fopen function is a file handle.  You can think of a file handle as a special value which refers to the open file.  (If you think of the file as a briefcase, then the file handle is the handle that allows you to pick up the briefcase and access its contents.)

You will want to store the file handle in a variable.  The type of a file handle is `FILE *`.  You can read this type as "pointer to file".

You will need to check the file handle returned by fopen to see if the file was actually opened.  You can treat the file handle value as though it were a boolean value: it will be true if the file was opened, or false if the file could not be opened.  E.g.:

{% highlight cpp %}
FILE *in = fopen("myfile.txt", "r");
if (!in) {
    fprintf(stderr, "Couldn't open the input file\n");
    exit(1);
}
{% endhighlight %}

After you are done reading from or writing to a file, the program should close the file:

<pre>
fclose( <i>filehandle</i> )
</pre>

So, a program that reads text data from a file might look like this:

{% highlight cpp %}
FILE *in = fopen("myFile.txt", "r");
if (!in) {
    fprintf(stderr, "Couldn't open the input file\n");
    exit(1);
}

// code that reads from the file

fclose(in);
{% endhighlight %}

## File I/O functions

The good news about reading from and writing to files is that the functions you can use functions that are equivalent to printf, scanf, etc.  The only thing that's different is that you'll need to pass the file handle as an argument.

Output to a file:

<pre>
fprintf( <i>file handle</i>, <i>format string</i>, <i>list of values</i> )
</pre>

Formatted input from a file:

<pre>
fscanf( <i>file handle</i>, <i>format string</i>, <i>list of variables</i> )
</pre>

Read the next character from a file and return its code (returning a negative value if no more characters):

<pre>
fgetc( file handle )
</pre>

So, `fprintf` is like `printf`, `fscanf` is like `scanf`, and `fgetc` is like `getchar`.

The `feof` function takes an input file handle as its argument, returns true if the file is known to be at end-of-file, false otherwise:

<pre>
feof( <i>file handle</i> )
</pre>

## Standard handles

The standard handles are file handles that automatically exist when your program starts.  You don't need to open them explicitly:

* `stdout` &mdash; the "standard output" handle
* `stdin` &mdash; the "standard input" handle
* `stderr` &mdash; the "standard error output" handle

You have used the standard handles in every program so far:

* `printf(...)` is equivalent to `fprintf(stdout, ...)`
* `scanf(...)` is equivalent to `fscanf(stdin, ...)`
* `getchar()` is equivalent to `fgetc(stdin)`

## Complete example

Count the number of occurrences of the letter Q in a file:

{% highlight cpp %}
FILE *in;
int ch, count;

count = 0;

in = fopen("pandp.txt", "r");
if (!in) {
	fprintf(stderr, "Couldn't open input file\n");
	exit(1);
}

while (!feof(in)) {
	ch = fgetc(in);
	if (ch == 'Q') {
		count++;
	}
}

printf("There were %i occurrences of 'Q'\n", count);

fclose(in);
{% endhighlight %}

<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->
