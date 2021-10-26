# How to install DFTB+?

There are different ways to install the DFTB+ software package on your local computer or cluster. In [this link](), there are several instruction that you
can use to install DFTB+. The DFTB+ version that can do the time-dependent excited state calculations, one needs to compile it with `ARPACK` library which 
is a library for computing the eigenvalues and eigenvectors of large matrices. Here are some instructions for installation of DFTB+ with `ARPACK`.

On of the most important thing is to use the same compilers in each step, both for compiling DFTB+ and `ARPACK`. Sometimes the compilers in 
`conda` environment may interfere with the compilers you have installed manually. To make the installation easier here, we only use the compilers installed 
with `conda install`. This can help you to avoid the complications you may face in manually installing everthing. 
