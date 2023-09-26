
## Recommended Installation for KLEE

You might be able to install klee and its dependencies locally via `snap install klee`.
However, after some troubles with snap and certain dependencies, we recommend first installing [Docker](https://docs.docker.com/engine/install/) and then building an image with KLEE's Dockerfile in their repository.
Reference KLEE's [Docker documentation](https://klee.github.io/docker/) for more information.

Once Docker is installed, you should be able to copy any files into the repository, build the image, run and access those files inside the container.

```bash
git clone git@github.com:klee/klee.git
mv <files> -t klee
cd klee
docker pull klee/klee:3.0
docker build -t klee/klee .
docker run --rm -ti klee/klee
```

Then you can compile with access to KLEE and its dependencies.

```bash
clang -emit-llvm -g -c program.c -o program.bc
klee program.bc
```

Exit the container with `exit`.

## interpreter.c

There's an added define in `interpreter.c` which will disable all print statements.
This makes KLEE's output more clear and helps speed up the fuzzing.
Pass the define flag `-DFUZZING` with `clang` to compile without the output from `interpreter.c`.
