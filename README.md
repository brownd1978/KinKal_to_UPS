# KinKal_to_UPS
Tools to build the KinKal package and install it in UPS.

# Introduction

* cd clean_working_dir
* git clone git@github.com:kutschke/KinKal_to_UPS.git
* setup mu2e
* KinKal_to_UPS/build -h

There are two ways to use this package:
  1) If you already have an exisiting build, you can create a UPS repository and install the existing build there.
  2) Start with nothing, clone, checkout, and, for both build prof and debug, build, test and install.

## Instructions for case 1

The simplest example for this case is that you have a working directory that contains 2 directories:
  KinKal build_debug
and you already have a debug version of root setup in the environment.  cd to that directory and do
the following:

* git clone git@github.com:kutschke/KinKal_to_UPS.git
* KinKal_to_UPS/build -h
* KinKal_to_UPS/build -v <git_tag_name> -i

This says to install the already built git tag and into the default UPS repository, which is ./artexternals;
it will be created if necessary.  The git tag is needed in order to name the UPS product version - more on
that later.

For example, if git_tag_name is v0.1.1, the UPS installation will be located at:
  artexternals/KinKal/v00_01_00

To use this UPS product:

* export PRODUCTS=${PWD}/artexternals
* ups list -aK+ KinKal
* setup -B KinKal <version> -q<qualifiers>

## Instructions for Case 2

In this case start in a clean working directory with no version of root or cmake already setup.

* git clone git@github.com:kutschke/KinKal_to_UPS.git
* setup mu2e
* KinKal_to_UPS/build -h
* KinKal_to_UPS/build -v "v0.1.1" -b -t -i -c "v3_18_2" -r "v6_20_08a -q+e20:+p383b:+prof" -j 24   -d ${PWD}/artexternals

This will do the following
* For the requested git tag of KinKal this will build, run the tests and install the built code into UPS.
* The ups repository into which it is installed is given by the -d option; the default is ${PWD}/artexternals.
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
