


http://isse.sourceforge.net/wiki/index.php/Linux_Developer

http://bitbucket.org/eigen/eigen/get/3.3-alpha1.tar.bz2


Hi, Bryan! This has been a while ago, I have successfully used Juce 3.2.0 and some other version, that I can't identify right now.


 kotowvr - 2015-09-28
Hi, there!
In case you're interested, I just tried to compile ISSE under Ubuntu 14.04, here's what I had to do:
1) start off with Linux developer page of isse project, and download what they say:
http://isse.sourceforge.net/wiki/index.php/Linux_Developer
You can also put Eigen and Juce manually into respective folders inside ../isse-code/sdks/
2) then you have to edit several files:
comment out the line
#include "effects/juce_FFT.h"
in ../isse-code/sdks/juce/modules/juce_audio_basics/juce_audio_basics.h
and ../isse-code/sdks/juce/modules/juce_audio_basics/juce_audio_basics.cpp
This will remove the name conflict between FFT class of ISSE and Juce
add a semicolon after command jassertfalse in line 305 of file
../isse-code/src/plugin/FilterGraph.cpp
3) compile as recommended in developer's wiki






Linux Developer
Jump to: navigation, search

Compiling for Linux has been tested on Fedora 16 and 19.
Contents

    1 Download Instructions
    2 Build Instructions
    3 Run Instructions
    4 Installation Instructions
    5 Third Party Dependencies

Download Instructions

    Open a command line and type:

        git clone git://git.code.sf.net/p/isse/code isse-code 
        cd isse-code 
        git submodule init sdks/juce 
        git submodule init sdks/eigen 
        git submodule update 

    Note, you should type the exact, individual submodule init/update commands, and not just "git submodule init" and "git submodule update". For the linux build, the submodule called "extras" is not needed (it maintains all of the necessary files for an osx and windows build). 

Build Instructions

    If needed, install the third party dependencies below.
    To build ISSE (64bit), type:

        cd builds/Linux 
        export CONFIG=Release 
        export TARGET_ARCH=-m64 
        make 

    To build a 32-bit version, type:

        cd builds/Linux 
        export CONFIG=Release 
        export TARGET_ARCH=-m32 
        make 

    To build both a 64-bit and 32-bit version, type:

        cd builds/Linux 
        mkdir 32 
        mkdir 64 
        export CONFIG=Release 
        export TARGET_ARCH=-m32 
        make 
        cp build/ISSE 32/ISSE 
        rm -rf build 
        export TARGET_ARCH=-m64 
        make 
        cp builds/ISSE 64/ISSE 

    Note, you may need to copy the remove the Linux/build folder if compiling the 32 after 64 bit version. 

Run Instructions

    To run the compiled executable (after running the build instructions), type:

        cd build 
        ./ISSE 

    Note, the final, compiled executable can be found at isse-code/builds/Linux/build/ISSE. 

Installation Instructions

    If you built the Linux project, there are dynamic libraries that need linking. Install as required per platform. 


Third Party Dependencies

    Special third party dependencies: fftw3 and jack
    On Fedora, type:

        sudo yum install jack-audio-connection-kit-devel jack-audio-connection-kit 
        sudo yum install fftw3-devel 








