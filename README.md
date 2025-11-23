# Third party halide
Third party gradle packaging for halide

## Updating thirdparty library version

### TODO


## Build Steps

1. Configure LLVM

```
cmake -G Ninja -S llvm-project/llvm -B buildLLVM \
        -DCMAKE_BUILD_TYPE=Release \
        -DLLVM_ENABLE_PROJECTS="clang;lld;clang-tools-extra" \
        -DLLVM_ENABLE_RUNTIMES=compiler-rt \
        -DLLVM_TARGETS_TO_BUILD="WebAssembly;X86;AArch64;ARM;Hexagon;NVPTX;PowerPC;RISCV" \
        -DLLVM_ENABLE_ASSERTIONS=ON \
        -DLLVM_ENABLE_EH=ON \
        -DLLVM_ENABLE_RTTI=ON \
        -DLLVM_ENABLE_HTTPLIB=OFF \
        -DLLVM_ENABLE_LIBEDIT=OFF \
        -DLLVM_ENABLE_LIBXML2=OFF \
        -DLLVM_ENABLE_TERMINFO=OFF \
        -DLLVM_ENABLE_ZLIB=OFF \
        -DLLVM_ENABLE_ZSTD=OFF \
        -DLLVM_BUILD_32_BITS=OFF
```

2. Build LLVM

```
cmake --build buildLLVM
```

3. Install LLVM

```
cmake --install buildLLVM --prefix installLLVM
```

4. Configure Halide

```
cmake -G Ninja -S Halide -B buildHalide \         
        -DCMAKE_BUILD_TYPE=Release \
        -DHalide_LLVM_ROOT=installLLVM \
        -DHalide_WASM_BACKEND=OFF \
        -DWITH_SERIALIZATION=OFF \
        -DWITH_DOCS=OFF \
        -DWITH_PYTHON_BINDINGS=OFF \
        -DWITH_TESTS=OFF \
        -DWITH_TUTORIALS=OFF
```

5.  Build Halide

```
cmake --build buildHalide
```

6. Install Halide

```
cmake --install buildHalide --prefix installHalide
```
