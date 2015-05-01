---
layout: default
title: "Lecture 21: Character strings"
---

# Character Strings

A string is a sequence of characters.

We have seen that a string literal can be used to represent a string that is known at the time the program is written:

{% highlight cpp %}
in = fopen("myfile.txt", "r");
{% endhighlight %}

There are lots of situations in which we'd like to be able to represent strings whose values are not known until the program is actually executed.  To store the value of a string, we need a data type that can represent a sequence of characters.

An array of char elements is a good data type for storing the value of a string.  There are two related issues we need to think about when using an array of char to store a string:

1.  How large should the array be?  This will determine the maximum length of the string we can store in the array.

2.  How do we know how long the string stored in the array is?  It could be less than the size of the array, in which case we need to know how many array elements are being used to store characters that are part of the string, and how many are just "extra space" at the end of the array.

There is no general answer to the first issue.  The most common approach is to make the array "large enough" that it will be able to store any string the program will need to handle.  Figuring out how large is large enough is not an easy question.

There are various approaches we could use to resolve the second issue.  We could require a string to be represented as two separate variables:

* The array
* An int variable storing the string's length

This would be cumbersome.

We could define a struct type to represent strings:

{% highlight cpp %}
struct String {
    char arr[MAXLEN];
    int len;
};
{% endhighlight %}

This is an attractive approach.  However, how large should MAXLEN be?  If it's too small, then programs can't handle some strings that they need to be able to store.  If it's too large, then the program might waste a lot of memory.  In general, we can't come up with a single, fixed answer for how large strings need to be.

The approach that C uses is to place a special terminator character at the end of each string.  The terminator is the NUL character, which is the character whose character code is 0.  You can specify the NUL character as a character literal like this: `'\0'`

Example: constructing the string "Hello"

{% highlight cpp %}
char str[100];
str[0] = 'H';
str[1] = 'e';
str[2] = 'l';
str[3] = 'l';
str[4] = 'o';
str[5] = '\0';
{% endhighlight %}

In memory, the array str looks like this:

> TODO: diagram

So, str is a char array of 100 elements storing a string of length 5.

Because the NUL terminator occupies one element of storage, the maximum length string that can be stored in an array of char elements is one less than the size (number of elements) of the array.

A string literal can be used as an array initializer:

{% highlight cpp %}
char str[100] = "Hello";
{% endhighlight %}

This is a more convenient way of achieving the same effect as above.

In fact, string literals (i.e., double quoted strings) are actually arrays of characters.  The characters making up the strings are terminated by a NUL character.  You can observe this property directly by using the array subscript operator on a string literal:

{% highlight cpp %}
char c = "Hello"[0];
printf("%c\n", c); // prints "H"
{% endhighlight %}

## size\_t

Note that quantities like array sizes or string lengths cannot be negative.  C makes use of this fact by defining a special integer type to represent lengths and sizes, called size\_t.  Size\_t is an unsigned type, meaning that it cannot represent negative values.

## String functions

C has a large number of functions that allow you to work with strings.

Danger!

One of the most common kinds of bugs in C programs is trying to store a string in an array that is too small.  For example, if your program tries to store a string of length 100 in a char array whose size is 80, the string will "overflow" the array.  When a string overflows an array, the result is unpredictable.  Sometimes (if you're lucky) the program will crash right away.  Other times, other variables in the program will be overwritten, meaning that their values mysteriously change.

So, you will have to be very careful not to overflow arrays in which your program stores string values.

### strlen

The strlen function takes a string as a parameter and returns the length of the string.  Prototype:

{% highlight cpp %}
size_t strlen(const char s[]);
{% endhighlight %}

Example:

{% highlight cpp %}
printf("%i\n", strlen("Hello")); // prints "5"
{% endhighlight %}

### strcmp

The strcmp function compares the values of two strings.  It returns 0 if the strings are equal, a positive value if the first string is "greater than" the second, and a negative value if the first string is "less than" the second.

The notions of "greater than" and "less than" are based on lexicographical comparision.  This is the same kind of comparison used to order words in a dictionary.

Prototype:

{% highlight cpp %}
int strcmp(const char s1[], const char s2[]);
{% endhighlight %}

One of the most important uses of `strcmp` is to test whether a character array contains a particular string values:

{% highlight cpp %}
char command[MAXLEN];

...

if (strcmp(command, "quit") == 0) {
    quit = true;
}
{% endhighlight %}

Another example, this time showing ordering between compared strings:

{% highlight cpp %}
char s1[] = "Apples";
char s2[] = "Oranges";

int cmp = strcmp(s1, s2);
if (cmp < 0) {
    printf("%s comes before %s\n", s1, s2);
} else if (cmp > 0) {
    printf("%s comes after %s\n", s1, s2);
} else {
    printf("%s is the same as %s\n", s1, s2);
}
{% endhighlight %}

In this example, the output

    Apples comes before Oranges

will be printed.  If you change the initializers for `s1` and `s2`, the other outputs are possible.


### printf, fprintf

The `%s` conversion specifier is used to print a string stored in a char array.

Examples:

{% highlight cpp %}
char str[100] = "Foobar";
printf("str contains %s\n", str);
fprintf(stdout, "str contains %s\n", str);
{% endhighlight %}

### scanf

The `%s` conversion specifies is used to read a series of non-whitespace characters into a char array.

Danger!

If the input sequence contains too many characters, it will overflow the array.

Example:

{% highlight cpp %}
char fname[200];
char lname[200];
printf("Enter your first and last names: ");
scanf("%s %s", fname, lname);
printf("Your initials are %c%c\n", fname[0], lname[0]);
{% endhighlight %}

NOTE!  You do not need to use an ampersand when reading string values into arrays using the `%s` conversion.

### fgets

The fgets function reads a line of input from an input file.  Prototype:

{% highlight cpp %}
char *fgets(char s[], int size, FILE *in)
{% endhighlight %}

The size parameter specifies the size of the array into which the string will be read.  It is used to ensure that the number of characters read does not overflow the array.

Example (reading an entire line of text from the keyboard):

{% highlight cpp %}
#define MAXLINE 200

...

char line[MAXLINE];
printf("Enter a line of text:\n");
fgets(line, MAXLINE, stdin);
{% endhighlight %}

Note that if the input line ends with a newline character `'\n'` (which it normally will), the character string stored in the array will have the newline character at the end.

### strcpy

The `strcpy` function copies the characters of a source string into a destination array.

Prototype:

{% highlight cpp %}
char *strcpy(char dest[], const char src[]);
{% endhighlight %}

Example:

{% highlight cpp %}
char name[200];
char name_copy[200];

printf("What is your name? ");
scanf("%s", name);

strcpy(name_copy, name);

name_copy[0] = 'W';

printf("If your name (%s) began with W instead of %c, it would be %s\n",
    name, name[0], name_copy);
{% endhighlight %}

Note: bad things happen if the source string is too large to store in the destination string!

### snprintf

The `snprintf` function does formatted output to a string.  It is very similar to `printf` and `fprintf`, but writes the output characters into a character array rather than sending them to a stream or file.

Prototype:

{% highlight cpp %}
int snprintf(char *str, size_t size, const char *format, ...);
{% endhighlight %}

Example:

{% highlight cpp %}
#define MSG_LEN

int num_apples;
double unit_price;
char msg[MSG_LEN];

printf("how many apples? ");
scanf("%i", &num_apples);

printf("unit price? ");
scanf("%lf", &unit_price);

snprintf(msg, MSG_LEN, "%i @ $%.02f each: $%.02f",
        num_apples, unit_price, num_apples * unit_price);

printf("%s\n", msg);
{% endhighlight %}

The `snprintf` function has one significant limitation.  If `size` or more output characters are copied into the array, then `snprintf` does *not* add a NUL terminator character to the string.  A string without a NUL terminator could lead to bugs later in the program, because subsequent functions applied to the string will not be able to determine the string's length.  One possible workaround is to always place a NUL character in the last element of the array:

{% highlight cpp %}
snprintf(msg, MSG_LEN, "%i @ $%.02f each: $%.02f",
        num_apples, unit_price, num_apples * unit_price);
msg[MSG_LEN-1] = '\0';
{% endhighlight %}

<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->
