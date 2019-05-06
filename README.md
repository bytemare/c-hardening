# Hardening C builds

A set of compilation options for hardening C builds with gcc.

## Use

### With CMake

Specify your desired CMake version and the .c files you want to build your project with, and indicate the include directory.

Then,

```sh
mkdir build
cd build
cmake ..
make
```

This will build your project and will pop warnings when something went wrong.

## Details

### Compilation warnings

- -W
- -Wall
- -Wextra
- -Werror
- -ansi
- -pedantic
- -Wuninitialized
- -Wcast-align
- -Wmissing-braces
- -Wunused-result
- -Wpointer-arith
- -Wchkp
- -Wl,-z,relro
- -Wl,-z,now
- -Wl,-z,noexecstack
- -Wstack-protector
- -Wformat
- -Wformat-security
- -Wstrict-aliasing
- -Wunused-parameter

### Security flags

Sanitizers

- -fsanitize=address
- -fsanitize=leak
- -fsanitize=undefined

Others

- -fstack-protector-strong (or -fstack-protector-all)
- --param ssp-buffer-size=1
- -pie (or -fpic)
- -fPIE
- -D_FORTIFY_SOURCE=2
- -fstack-check
- -fsplit-stack

### Performance

Performance flags (may have security impact)

-finline-functions
-O2

### Other Recommendations

- You may want to use more libbsd functions than the standard c library. For this, look up your desired functions in the manual, install libbsd-dev or (use ```$(pkg-config --libs libbsd)``` ), and link with ```-lbsd```.
- Try to break your program on purpose with known bad input and envrionnment.
- Fuzz your inputs with random data and observe if your program handles weird input.
- Kill your program in the middle of an operation and observe how it behaves afterwards (are log files unlocked ? sockets closed ?)
- Evaluate if the choices you made are really the best for your specific use case.
- Always re-evaluate and ask yourself if you're not doing too much. Then answer objectively.
- Most importantly : isn't there alread something else out there that does what you intend to do, but maybe better ? ;-)
