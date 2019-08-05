# Mirage-Baremetal-RiscV

---

This repository demonstrates the steps required to build and simulate Mirage unikernels on baremetal RiscV

## What

### hello_world

Prints "Hello!" every second to demonstrate the most basic Mirage unikernel.


## Requirements

- installed instance of [shakti-tee-tools](https://gitlab.com/shaktiproject/tools/shakti-tee/shakti-tee-tools).


## How

This remains experimental but I've done a lot to make the process as simple as possible.

### Requirements

- installed instance of [shakti-tee-tools](https://gitlab.com/shaktiproject/tools/shakti-tee/shakti-tee-tools).

### Build a kernel

* Switch to ocaml4.07.0 compiler : 
`opam switch 4.07.0`
* Add my custom opam repository for esp32 packages: 
`opam repo add opam-cross-shakti git@github.com:mirage-shakti-iitm/opam-cross-shakti.git`
* Install mirage configuration tool. 
`opam install mirage`
* Go in the unikernel directory that you want to run and type the following commands:
```
mirage configure -t riscv
make depends
mirage build
make kernel
```

 Currently the `mirage build` generates the `main.native.o` of RiscV type and does not link anything further. The linking step is taken care of `make kernel` which generates `rv64` ELF file, `kernel` which can be simulated on [spike](https://gitlab.com/shaktiproject/tools/shakti-tee/shakti-tee-isa-sim)
 
### Run a kernel

`spike kernel`


#### Note
The packages ported out in `opam-cross-shakti` custom repository support building simple unikernel applications like `hello-world` . Further packages to support other applications are being ported out.