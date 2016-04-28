#Installation Manual for MacOS

* Install [brew](http://brew.sh/) runing `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"` (Package manager for MacOS) 
* Install git `brew install git`

## Clone this repo

Fork the master [repo](https://github.com/oliverlee/phobos) into your GitHub account and clone it in your computer. Create a folder named `/build` in the root of the cloned repo `mkdir build` 

Once you have cloned the forked repo in your pc, it is good practice to keep the fork synced with the master repo. To do this create a remote link to the master `git remote add oliverlee git@github.com:oliverlee/phobos.git`. You can now update your local repo with the latest modifications made in the master repo using `git fetch oliverlee`. For furthre reading about remote repos please follow this [link](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)

## Toolchain Installation 
 Install cmake, eigen, boost and OpenOCD using brew `brew install cmake open-ocd eigen boost`
* Download the latest [GCC ARM Embedded toolchain](https://launchpad.net/gcc-arm-embedded/5.0/5-2016-q1-update/+download/gcc-arm-none-eabi-5_3-2016q1-20160330-mac.tar.bz2) (we are currently using version **5_3-2016q1**), and extract it in `cd ~/toolchain` `dtrx -vr [pathtoyourdownloadedfile]` (Install first dtrx _"Do The Rigth eXtraction"_ using `brew install dtrx`)
> When creating the CMake build tree, the compiler must be set to the target toolchain to allow cross-compilation. CMake cannot change the compiler after the build tree has been created and if the toolchain is not provided, the default compiler will be used. The path to the toolchain must be defined in a CMake script file and passed as in the argument `CMAKE_TOOLCHAIN_FILE` the first time cmake is called.
    * Run `cmake -DCMAKE_TOOLCHAIN_FILE=../toolchain-gcc-arm-none-eabi-5_3-2016q1.cmake ..` from the `build` directory
    * If you get an error, try modifying the build options accordingly to the error  using `ccmake .` (A GUI showing you the set values for the options will appear).
    * Modify the file `random.tcc` under `~/toolchain/gcc-arm-none-eabi-5_3-2016q1/arm-none-eabi/include/c++/5.3.1/bits/random.tcc` has to be modified as described [here](https://gcc.gnu.org/bugzilla/attachment.cgi?id=36237&action=diff)
    * Run `make -j8`.

## Eclipse Installation

* Make sure command line tools are installed. (Check `pkgutil --pkg-info=com.apple.pkg.CLTools_Executables` in the terminal to be sure you have it, otherwise run `xcode-select –install`)
* Install latest java [JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* Install latest [Eclipse IDE C/C++ for developers](http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/mars/2/eclipse-cpp-mars-2-macosx-cocoa-x86_64.tar.gz) 
* 

