# KinKal_to_UPS
Tools to build the KinKal package and install it in UPS.

# Introduction

There are two basic ways to use this package:
  1) If you already have an exisiting build, you can create a UPS repository and install the existing build there.
  2) Start with nothing, clone, checkout, and, for both build prof and debug, build, test and install.

## Instructions for case 1

The simplest example for is that you have a working directory that contains 2 directories:

  KinKal build_debug

and you already have a UPS debug version of root set up in the environment.  In that directory and do
the following:

* git clone git@github.com:kutschke/KinKal_to_UPS.git
* KinKal_to_UPS/build -h  # to get help
* KinKal_to_UPS/build -v <git_tag_name> -i

This will look for the source for KinKal in the subdirectory KinKal and the built debug version in
the subdirectory build_debug.  It will install the already built git tag and into the default UPS
repository, which is ./artexternals; the UPS repository will be created if necessary.  The git tag
is needed in order to name the UPS product version.

For example, if git_tag_name is v0.1.1, the UPS installation will be located at:

   artexternals/KinKal/v00_01_00

and the UPS qualifiers will be copied from the underlying root UPS pacakge.

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
* It will use the indicated versions of cmake and root; there is a default for cmake but only sort-of for root (see below).
* The make step will do a 24 way parallel build, which is appropriate for mu2ebuild01
* It will build both prof and debug; it knows that cmake spells these Release and Debug.
* It assumes that debug version of ROOT differs from the prof version by the exchange prof->debug in the qualifier string
* If you omit the -r qualifier, and if there is already a version of root set up in the environment, this command will only build and install one of prof/debug, the one matching the version of root already set up.

When this is complete you will see the following subdirectories of clean_working_dir
* KinKal_to_UPS - this package
* KinKal        - the cloned source
* build_prof    - the working space for the Release (prof) build
* build_debug   - the working space for the Debug (debug) build
* artexternals  - the UPS repo into which the code is installed.

You can point the UPS repo at an arbitrary directory using the -d option but the other four directory names are hard coded.

The default behaviour is to abort if the KinKal directory already exists; it will overwrite existing files in build_prof, build_debug
and artexternals/KinKal.

## Fixmes, Todos and questions

* Is there a better name than KinKal_to_UPS?
* Should KinKal_to_UPS be installed in UPS?
* In the case of installing a prebuilt version of KinKal, is there a way to automatically determine the git tag so that it does not need to be given by hand in the install command?
* Add an option to add additional qualifiers to the KinKal product
* Is it OK that the names build_prof, build_debug are hard coded?  If not, we can make options to define them.

