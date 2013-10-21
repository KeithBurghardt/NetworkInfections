NetworkInfections
=================

Code for simulating infections on Lattice, Random (Erdos-Renyi and Poisson configuration model),
Small World (WS), Scale-free (BA and configuration model), and 1000-node real networks, 
via NetLogo (all models except for configuration models) and C (configuration models only).

To use the Netlogo code (.nlogo) get the latest netlogo version, and if necessary, the latest version of Java.
There is an option for a Mathematica link (I have some code for this which I have not commented well). In addition,
there are Configuration models written in C, which need the GNU compiler and GSL (GNU Scientific Library). 

The C code has been optimized for speed, but will work best with the following flags:  
  -gsl -lgslcblas -pthread -03 -funroll-loops [possible -fvariable-expansion-in-unroller]
  
For additional speed, we recommend using HOARD (or similar malloc parallel memory allocator) if the user intends to 
use ammend this code to allocate memory a significant number of times. As-is, however, memory allocation is only called 
at the beginning of the code thus will not be slowed down significantly without a parallel memory allocator.
  
These flags are in order from mandatory to optional. gcc cannot compile without the -gsl and -lgslcblas flags 
(at least on the linux servers we use which reference the libraries from a non-standard directory). The code will also be
very slow unless the -pthread flag is used for parallel threading. Of the many optimization flags, we find that -O3 can 
improve speed by a factor of 2 or more, while -funroll-loops increases speed by an additional ~20% in small network
samples.


With present computer speeds, this C code can easily handle a somewhat coarse grain behavior space of 10^6 nodes while
the Netlogo code can easily handle ~10^4 nodes (although this might be improved).
