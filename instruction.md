## install tools

> sudo apt-get install build-essential cmake git libgmp3-dev libprocps4-dev python-markdown libboost-all-dev libssl-dev

## install dependency from github

> git submodule init

> git submodule update

## create build directory, create makefile with cmake

> mkdir build

> cd build

> cmake ..

## make file.

> make

> make `module name`

> make profile_r1cs_ppzksnark


## run executable file

> cd build/libsnark

> ./profile_r1cs_ppzksnark 1000 10 Fr


# steps of theory
Using the library involves the following high-level steps:

1. Express the __statements__ to be proved as an R1CS (or any of the other languages above, such as arithmetic circuits, Boolean circuits, or TinyRAM). This is done by writing C++ code that constructs an R1CS, and linking this code together with libsnark
2. Use libsnark's __generator algorithm__ to create the __public parameters__ for this statement (once and for all).
3. Use libsnark's __prover algorithm__ to __create proofs__ of true statements about the satisfiability of the R1CS.
4. Use libsnark's __verifier algorithm__ to __check proofs__ for alleged statements.
