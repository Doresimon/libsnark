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
