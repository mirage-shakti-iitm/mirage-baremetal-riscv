FROM iitmshakti/riscv-ocaml-baremetal:0.1.0
WORKDIR home/mirage-user
ENV RISCV /install
ENV PATH "$RISCV/bin:${PATH}"
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:avsm/ppa
RUN apt update
RUN apt install -y opam
RUN opam init --disable-sandboxing --compiler=4.07.0
RUN eval $(opam env)
RUN opam repo add opam-cross-shakti https://github.com/mirage-shakti-iitm/opam-cross-shakti.git
RUN opam install mirage.3.5.0 -y
RUN git clone -j 32 --depth=1 https://github.com/mirage-shakti-iitm/mirage-baremetal-riscv.git
WORKDIR mirage-baremetal-riscv/hello-world
RUN eval $(opam env)
RUN opam install mirage
RUN eval $(opam env)
RUN opam config exec -- mirage configure -t riscv
RUN make depends
RUN eval $(opam env)
RUN opam install num-riscv
RUN opam config exec -- mirage build
RUN eval $(opam env)
RUN make kernel
RUN echo "Testing on spike:"
RUN spike kernel