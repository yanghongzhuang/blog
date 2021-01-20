

#### 1. Targets
```
$ make
nasm -o loader.bin -f bin loader.asm
rustc -O --target i386-intel-linux --crate-type lib -o main.o --emit obj main.rs
error: Error loading target specification: Could not find specification for target "i386-intel-linux". Use `--print target-list` for a list of built-in targets

Makefile:13: recipe for target 'main.o' failed
make: *** [main.o] Error 1
```