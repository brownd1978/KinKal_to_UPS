# KinKal_to_UPS
Tools to build the KinKal package and install it in UPS.

There are two ways to use this package:
  1) Start with nothing, clone, checkout, and, for both build prof and debug, build, test and install.
  2) If you already have an exisiting build, you can install the existing build.


Instructions for Case 1

* cd clean_working_dir
* git clone git@github.com:kutschke/KinKal_to_UPS.git
* setup mu2e
* KinKal_to_UPS/build -h

For example:
KinKal_to_UPS/build -v "v0.1.1" -b -t -i -c "v3_18_2" -r "v6_20_08a -q+e20:+p383b:+prof" -j 24   -d ${PWD}/artexternals

* For the indicated git tag of KinKal this will build, run the tests and install the built code into UPS.
* The ups repository into which it is installed is given by the -d option.
* It will use the indicated versions of cmake and root
* The make step will do a 24 way parallel build, which is appropriate for mu2ebuild01
* It will build both prof and debug; it knows that cmake spells these Release and Debug.
* It assumes that debug version of ROOT differs from the prof version by the exchange prof->debug in the qualifier string

When this is complete you will see the following subdirectories of clean_working_dir
* KinKal_to_UPS - this package
* KinKal        - the cloned source
* build_prof    - the working space for the Release (prof) build
* build_debug   - the working space for the Debug (debug) build
* artexternals  - the UPS repo into which the code is installed.

You can point the UPS repo at an arbitrary directory using the -D option but the other four directory names are hard coded.

Instructions for case 2:




