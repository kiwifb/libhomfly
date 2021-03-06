# libhomfly
## Library to compute the homfly polynomial of a link.

This is basically a conversion of the [program][1] writen by Robert J Jenkins Jr into a shared library. It accepts as entry a character string, formated in the same way as the input files that the original code used (see below). The returned value is the string that the original program did print on screen.

The modifications done to the original program are:

* modified input/output to allow being called as a shared library
* the library now does not write any output to stdout
* memory allocation moved to boehmgc to prevent memory leaks

### Authors:

* Robert J Jenkins Jr wrote the original program in 1990. The last version, used as a basis for this library was writen in 2010.
* Miguel Marco made the modifications to make it a library in 2015.


### Dependencies

* standard c library
* boehmgc

### Instalation

Type


````
autoreconf --install
````

to generate the config script. Then run


````
./configure
make
````

to build the library. Finally, as superuser run


````
make install
````

to install it. The autoreconf command should be in the autotools package.


### Example of usage

This simple program can be used as an example on how to use the library. In particular, it computes the homfly polynomial of the trefoil knot.

``````````````````````````````````````````````````````````````````````````````````````````
#include <stdio.h>
#include <stdlib.h>
#include "homfly.h"
#include <gc.h>

int main()
{
    char *out;
    char input[] = " 1 6 0 1 1 -1  2 1  0 -1  1 1  2 -1 0 1 1 1 2 1 ";
    out = homfly(input);
    printf("%s", out);
    return 0;
}
``````````````````````````````````````````````````````````````````````````````````````````

### Input format

Links are represented by a string with numbers separated by spaces as follows

* how many strings,
 * for each string, how many crossings, then
   * for each crossing, the cross name, then 1 if over, -1 if under
* for each crossing, the name of the crossing and 1 if right, -1 if left.

The spacing and placement of returns don't matter.  Integers only.
If there are n crossings, they must be named 0..n-1.

### License

The original program by Robert J Jenkins Jr is in the public domain, so i choose to keep it. This means in particular that you are free to distribute it or any derivative work under whichever license you choose.

[1]: http://burtleburtle.net/bob/knot/homfly.html
