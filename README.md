#PHOBOS
The larger and innermost of the two natural satellites of Mars, Phobos is the
embedded system that controls the gyroscopic balance assistance system.

## Toolchain
To compile the code, use [GNU ARM Embedded
toolchain](https://launchpad.net/gcc-arm-embedded).
The version used is 4.9-2015-q3.

There is a [known
issue](https://answers.launchpad.net/gcc-arm-embedded/+question/280242) in GCC
5.2 2015q4 with Link Time Optimization. Either use GCC 4.9 or disable LTO.

Some examples may not build as the option `-fsingle-precision-constant` is not
standard compliant. The issue is documented
[here](https://bugs.launchpad.net/gcc-arm-embedded/+bug/1452470) and contains a
fix.

As most computers will be running a 64-bit kernel, libraries for ia32/i386
architecture will need to be installed if not already. For recent versions of
Ubuntu, this can be installed with the `gcc-multilib` package.

## Building
When creating the CMake build tree, the compiler must be set to the target
toolchain to allow cross-compilation.  CMake cannot change the compiler after
the build tree has been created and if the toolchain is not provided, the
default compiler will be used.  The path to the toolchain must be defined in a
CMake script file and passed as in the argument `CMAKE_TOOLCHAIN_FILE` the first
time `cmake` is called.  An example file is provided in the root project
directory.

    oliver@canopus:~/repos/phobos$ mkdir build
    oliver@canopus:~/repos/phobos$ cd build/
    oliver@canopus:~/repos/phobos/build$ cmake -DCMAKE_TOOLCHAIN_FILE=~/toolchain/toolchain-gcc-arm-none-eabi-4_9-2015q3.cmake ..
    oliver@canopus:~/repos/phobos/build$ make -j8

Build options can be passed as arguments to `cmake` or set with `ccmake` after
the build tree has been created.

    oliver@canopus:~/repos/phobos/build$ ccmake .

## Flashing
The compiled ELF can be flashed to the microcontroller by enabling the
`OPENOCD_FLASH_TARGET` or `OPENOCD_FLASH_AND_RUN_TARGET` CMake options.

If you are running OSX and unable to flash successfully with CMake, OpenOCD may
be requesting to receive incoming network connections. This can be done by
signing the application:

    oliver@canopus:~$ codesign --verify -vv /usr/local/Cellar/open-ocd/HEAD/bin/openocd

In 'Security & Privacy', verify that the option 'Automatically allow signed
software to receive incoming connections' is enabled.

## Debugging
The microcontroller can be debugged with OpenOCD and GDB.

    oliver@canopus:~/repos/phobos$ openocd -f openocd_olimex-arm-usb-tiny-h_stm32f4.cfg

In another shell instance, pass GDB the ELF as an argument

    oliver@canopus:~/repos/phobos/build$ ~/toolchain/gcc-arm-none-eabi-4_9-2015q3/bin/arm-none-eabi-gdb demos/usb_serial/ch.elf

To connect to target

    (gdb) target extended-remote localhost:3333

Additionally, the ELF can be flashed

    (gdb) load
    (gdb) mon reset init

There is an example `gdbinit` file in the root directory that defines a command
to connect to the remote and set hardware break/watch point limits in addition
to disabling IRQs while stepping. This can be used by renaming the file to
`.gdbinit` and placing in your home or project directory or by executing GDB
commands from a file when starting GDB

    oliver@canopus:~/repos/phobos/build$ ~/toolchain/gcc-arm-none-eabi-4_9-2015q3/bin/arm-none-eabi-gdb -x ../gdbinit demos/usb_serial/ch.elf

