# 1. How to install DFTB+?

There are different ways to install the DFTB+ software package on your local computer or cluster. In the [DFTB+ github repository](https://github.com/dftbplus/dftbplus), there are several instruction that you
can use to install DFTB+. The DFTB+ version that can do the time-dependent excited state calculations, one needs to compile it with `ARPACK` library which 
is a library for computing the eigenvalues and eigenvectors of large matrices. You can also install DFTB+ using `conda` too but that version is also not capable
of doing excited states calculations. Here are some instructions for installation of DFTB+ with `ARPACK`.

On of the most important thing is to use the same compilers in each step, both for compiling DFTB+ and `ARPACK`. Sometimes the compilers in 
`conda` environment may interfere with the compilers you have installed manually. To make the installation easier here, we only use the compilers installed 
with `conda install`. This can help you to avoid the complications you may face in manually installing everthing. You first need to install `miniconda` or `anaconda`
and then create an environment to use install and use different packages. The instructions for miniconda is brought in Libra installation in [this link](https://github.com/Quantum-Dynamics-Hub/libra-code/tree/devel).

Use the following instructions for compiling the DFTB+ with `ARPACK`.

**1.1** Install the Fortran and C/C++ compilers using `conda`:
```
conda install cmake
conda install gcc_linux-64
conda install gxx_linux-64
conda install -c anaconda gfortran_linux-64 
conda install -c conda-forge/label/gcc7 arpack 
```
 
**1.2** Make a separate directory and download the latest version of DFTB+ and extract the compressed file:
```
mkdir DFTB+; cd DFTB+
wget https://github.com/dftbplus/dftbplus/releases/download/21.1/dftbplus-21.1.tar.xz --no-check-certificate
tar xvf dftbplus-21.1.tar.xz
cd dftbplus-21.1
```
 
**1.3** Set the default `PATH` and `LIBRARY_PATH`s to the conda environment you use.
```
export PATH=/path/to/miniconda/envs/py37/bin:$PATH
export LD_LIBRARY_PATH=/path/to/miniconda/envs/py37/lib:$LD_LIBRARY_PATH
export LIBRARY_PATH=/path/to/miniconda/envs/py37/lib:$LIBRARY_PATH
 ```
 
**1.4** Use `cmake` for configuration and making the package.
```
rm -rf _build
FC=gfortran CC=gcc cmake \
-DWITH_ARPACK=true \
-DCMAKE_INSTALL_PREFIX=/path/to/installation/of/dftb+ -B _build .
```
Now build and install the package:
```
cmake --build _build -- -j
cmake --install _build
```
Then, download the needed files such as Slater-Koster files. You can install all other prerequisites by using:
```
./utils/get_opt_externals ALL
# or for just downloading the Slater-Koster files
./utils/get_opt_externals slakos
```
For downloading the basis set, which is used to generate the cube files in `waveplot`, you can use the following link:

https://dftb.org/parameters/download

**1.5** Use DFTB+

When you login to your account, you either want to use it in the bash file or submit it as job using `qsub` or `sbatch`. Here are the set of scripts
you need to add to your bash script or submit file:
```
cd /to/input/file/directory
export OMP_NUM_THREADS=number_of_processors
source $HOME/.bashrc # This is to activate miniconda and the environment you used to install DFTB+
export PATH=/path/to/installation/of/dftb+/bin:$PATH
dftb+ inputfile > out.log
```

All other executables are available in the `dftb+/bin` folder such as `waveplot` or `xyz2gen` or `gen2xyz`. To see all the executable files, you can use `ls dftb+/bin`.


