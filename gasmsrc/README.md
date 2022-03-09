# Defender (1981) by Eugene Jarvis and Sam Dicker

## Build Instructions

### Build Requirements
* Rust

### Build the assembler toolchain
We use [`gazm`](https://github.com/gazliddon/gazm) to assemble the main game source and [`vasm`](http://www.compilers.de/vasm.html) to compile the sound module. 

First you must run the following to set up the git submodules containing the assembler toolchain:

```sh
git submodule init
git submodule update
```

Now you can build the toolchain, as follows:

```sh
cd vasm-mirror
make CPU=6800 SYNTAX=oldstyle
cd ..
cd gazm
rustup run nightly build --release
cd ..
```
### Build Defender

