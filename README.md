# Peekaboo
peekaboo is an attempt to provide an easily extensible and usable dynamic trace
format. peekaboo provides definitions for typical properties expected for
dynamic traces like instruction addresses, memory operand info, register info,
etc. The trace is structured as a collection of files each corresponding to some
piece of information which the trace support. Currently, peekaboo has a
execution tracer that is built on top of DynamoRIO. There are future plans for a
PIN execution tracer and different conversion tools to convert traces obtained
from other tools to peekaboo format.

## Architectures
### Currently Support
AMD64, AARCH64
### Planned Support
X86, AARCH32

## libpeekaboo API
Build a static library:
```
cd libpeekaboo
make
```
APIs:
TODO

## For DynamoRIO
### How to build
DynamoRIO version must be higher than 7.90.17998
```
cd peekaboo_dr
mkdir build
cd build
DynamoRIO_DIR=($DynamoRIO_PATH) cmake ..
make
```
Then you will have a file named 'libpeekaboo_dr.so' under the build folder.
### Build with syscall trace plugin
This component requires Dr.Memory. (https://github.com/DynamoRIO/drmemory/wiki/Downloads)
```
DynamoRIO_DIR=($DynamoRIO_PATH) DrMemoryFramework_DIR=($DrMemory_drmf_path) cmake .. -DSYSCALL=ON
make
```
Before you run it, you need to add the directory of libdrsyscall.so to your LD_LIBRARY_PATH. It is likely to be inside DrMemory/drmf/lib64/ or DrMemory/drmf/lib32.
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:($libdrsyscall_DIR)
```
### How to run
Say, you want to run with command ls in 64-bit mode:
```
($DynamoRIO_PATH)/bin64/drrun -c ($Peekaboo_PATH)/peekaboo_dr/build/libpeekaboo_dr.so -- ls
```
