Notes for CMAKE build
=============================

The CMake build allows to generate LLVM bitcode for `libssl` and `libcrypto` that can be linked to test harnesses and symbolically executed by KLEE.

**NOTE**: This method is still WIP and attempting to build a regular (static or dynamic) library will inevitably result in undefined references.

## Build LLVM Bitcode
To generate `libssl.bc` and `libcrypto.bc`:
```bash
mkdir build
cd build

# Configure build for LLVM bitcode generation, also include bolt-taint
# You will need to install llvm-8 and clang-8 for this step
cmake -DCMAKE_BUILD_TYPE=Debug -WITH_APPS=OFF -DLLVM_BITCODE_ONLY=ON -DCMAKE_C_COMPILER=$PATH_TO_CLANG -DCMAKE_CXX_COMPILER=$PATH_TO_CLANG++ -DCMAKE_LINKER=$PATH_TO_LLVM_LINK -DKLEE_INCLUDE_DIR=../../../../include ..

# Build
make -kj
```
