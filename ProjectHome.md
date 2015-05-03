**SEE MY NEW GENERAL LP TOOL: http://code.google.com/p/nano-lp/**

# ypweb - literate programming tool #

## About ##

_Easy to understand, quick to start!_

Literate programming (LP) is an approach to programming introduced by Donald
Knuth as an alternative to the structured programming paradigm of the 1970s.
Idea is to write programs like an uninterrupted exposition of logic in an
ordinary human language, much like the text of an essay, in which macros which
hide abstractions and traditional source code are included. See for more
information: http://en.wikipedia.org/wiki/Literate_programming.

First version of ypweb tool is written on Python 3. The difference from standard
LP is that no macroses, so user can not write chunk of code and then include it
in another place. Why? Because it's excessively in LP, and is possible to use
macroses of your programming language or the templating system, not LP.

## Example ##

You write one file (.w) with usual text of your ideas, thoughts, concepts,
comments of code, figures inserting and code chunks. It seems like essay or
article. This file is written in reStructured Text format - usual text format
with some markup like Markdown, see http://en.wikipedia.org/wiki/ReStructuredText.

Code chunks begins with a special line with a marker (default is ;;) at the
start.  This line may consists of several pies, so these pies use a delimiter
(default ;).  Both (;; and ;) may be specified in a command line.

These pies are:

  * output file name for source code contained this code chunk
  * object (any name preferred by user, e.g, funs, defs...)
  * short caption/name

Example:

```
;; comport.h;defs;BAUDRATE
#define BAUDRATE 9600
```

Some pies may be omitted. If user omits file name then previous file name will
be used; if user omits file name and object then previous file name and object
will be used.

Empty special line (only marker ;;) ends code chunk and continues documentation.
Here is an example:

```
    ================================
    Example of features of the ypweb
    ================================

    Some definitions (macroses) used in COM module:
    ;; x.h; defs; COM definitions
    ;; Port number
    #define PORT 1
    ;; Baudrate
    #define BAUD 9600
    ;; funs; open()
    int open(char *name, char *mode);
    ;;
    "Opening" of COM (initializing, preparing of internal structs) is
    implemented in the next function. Arguments are:

    - name - name of the port
    - baud - baudrate (1200, 2400, 4800, 9600...)
    - databits - number of data bits
    - stopbits - number of stop bits
    - parity - parity is used or not (1, 0)
    ;; x.c; funs; open()
    int open(char *name, int baud, int databits, int stopbits, int parity) { \
        // some code is here ...
        return 0;
    }

    ;; x.h; defs; XXX
    #define XXX
    ;;
    That's all folks!
```

Run example:

```
python ypweb.py ex.w
```

Processing of this file produces 2 source files: x.h and x.c with some defs (definitions)
and funs (functions) and file with documentation in ReStructuredText format (the same
file name but with .rst extension). User can use it to make HTML of PDF files (with
rst2pdf tool or Python docutils, for example).

Output .rst file contains documentation part, formatted code chunks, indexes, links from
indexes to code chunks.

So, scheme of example is

```
ex.w --> ex.rst (--> ex.html/ex.pdf)
  +----> x.c, x.h
```

## Manifest ##

Tool is only one Python file (ypweb.py) so does not need any installation.
ex.w, ex.rst, ex.html, x.c, x.h - are files of example.