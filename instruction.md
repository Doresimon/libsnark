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

# R1CS ppzksnark example

3 entities: generator, prover, verifier

1. generator: run ppzksnark with **a given constraint system(CS)**, return a **proving key** and a **verification key**.
2. prover: run ppzksnark prover with **proving key**, **primary input**, **auxiliary input**: return **proof**.
3. verifier: run ppzksnark virifier with **verification key**, **primary input**, **proof**: return **true or false**.

# R1CS class

## class `r1cs_constraint_system`
* primary_input_size: `size_t`
* auxilisry_input_size: `size_t`
* constraints: `vector<r1cs_constraint>`

## class `r1cs_constraint`
* a: `linear_combination`
* b: `linear_combination`
* c: `linear_combination`

## class `linear_combination`
* terms: `vector<linear_term>`

## class `linear_term`
* index: `var_index_t`
* coeff: `filedT`

## class `variable`
* index: `var_index_t`

### `r1cs_ppzksnark_constraint_system` = `r1cs_constraint_system`
### `r1cs_ppzksnark_primary_input` = `r1cs_primary_input` = `std:vector<FieldT>`
### `r1cs_ppzksnark_auxiliary_input` = `r1cs_auxiliary_input` = `std:vector<FieldT>`


### `knowledge_commitment_vector` = `sparse_vector<konwledge_commitment<T1,T2>>`

## class `sparse_vector`
* indices: `vector<size_t>`
* values: `vector<T>`
* domain_size: `size_t`

## class `accumulation_vector`
* first: `T`
* rest: `sparse_vector<T>`

## class `r1cs_ppzksnark_proving_key`
* A_query: `knowledge_commitment_vector<G1<ppT>,G1<ppT>>`
* B_query: `knowledge_commitment_vector<G2<ppT>,G1<ppT>>`
* C_query: `knowledge_commitment_vector<G1<ppT>,G1<ppT>>`
* H_query: `G1_vector<ppT>`
* K_query: `G1_vector<ppT>`
* constraint_system: `r1cs_ppzksnark_constraint_system<ppT>`

## class `r1cs_ppzksnark_verification_key`
* alphaA_g2: `G2<ppT>`
* alphaB_g1: `G1<ppT>`
* alphaC_g2: `G2<ppT>`
* gamma_g2: `G2<ppT>`
* gamma_beta_g1: `G1<ppT>`
* gamma_beta_g2: `G2<ppT>`
* rC_Z_g2: `G2<ppT>`
* encoded_IC_query: `accumulation_vector<G1<ppT>>`

## class `r1cs_ppzksnark_keypair`
* pk: `r1cs_ppzksnark_proving_key`
* vk: `r1cs_ppzksnark_verification_key`

## class `r1cs_ppzksnark_proof`
* g_A: `knowledge_commitment<G1<ppT>,G1<ppT>>`
* g_B: `knowledge_commitment<G2<ppT>,G1<ppT>>`
* g_C: `knowledge_commitment<G1<ppT>,G1<ppT>>`
* g_H: `G1<ppT>`
* g_K: `G1<ppT>`

# R1CS example
## func generate_r1cs_example_with_filed_input(const size_t `num_constraint`, const size_t `num_input`): `r1cs_example` {...}
1. 
