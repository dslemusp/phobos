#Installation Manual for MacOS

* Install [brew](http://brew.sh/) runing `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"` (Package manager for MacOS) 
* Install git `brew install git`

## Clone this repo

Fork the master [repo](https://github.com/oliverlee/phobos) into your GitHub account and clone it in your computer. Create a folder named `/build` in the root of the cloned repo `mkdir build` 

Once you have cloned the forked repo in your pc, it is good practice to keep the fork synced with the master repo. To do this create a remote link to the master `git remote add oliverlee git@github.com:oliverlee/phobos.git`. You can now update your local repo with the latest modifications made in the master repo using `git fetch oliverlee`. For furthre reading about remote repos please follow this [link](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
## Toolchain Installation 
* Install cmake, eigen, boost and OpenOCD using brew `brew install cmake open-ocd eigen boost`
* Download the latest [GCC ARM Embedded toolchain](https://launchpad.net/gcc-arm-embedded/5.0/5-2016-q1-update/+download/gcc-arm-none-eabi-5_3-2016q1-20160330-mac.tar.bz2) (we are currently using version **5_3-2016q1**), and extract it in `tar [yourdownloadedfile] ~/toolchain/`.

## Eclipse Installation

* Make sure command line tools are installed. (Check `pkgutil --pkg-info=com.apple.pkg.CLTools_Executables` in the terminal to be sure you have it, otherwise run `xcode-select –install`)
* Install latest java [JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* Install latest [Eclipse IDE C/C++ for developers](http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/mars/2/eclipse-cpp-mars-2-macosx-cocoa-x86_64.tar.gz) 


* 

## Eclipse Installation

* Make sure command line tools are installed. (Check `pkgutil --pkg-info=com.apple.pkg.CLTools_Executables` in the terminal to be sure you have it, otherwise run `xcode-select –install`)
* Install latest java [JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* Install latest [Eclipse IDE C/C++ for developers](http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/mars/2/eclipse-cpp-mars-2-macosx-cocoa-x86_64.tar.gz) 


