# KinKal_to_UPS
Tools to build the KinKal package and install it in UPS.

Instructions:

cd working_dir
git clone git@github.com:kutschke/KinKal_to_UPS.git
setup mu2e
KinKal_to_UPS/build -h

For example:
KinKal_to_UPS/build -v "v0.1.1" -b -t -i -c "v3_18_2" -r "v6_20_08a -q+e20:+p383b:+prof" -j 24   -d ${PWD}/artexternals

* For the indicated git tag of KinKal this will build, run the tests and install the built code into UPS.
* The ups repository into which it is installed is given by the -d option.
* It will use the indicated versions of cmake and root
* The make step will do a 24 way parallel build, which is appropriate for mu2ebuild01
* It will build both prof and debug; it knows that cmake spells these Release and Debug.
* It assumes that debug version of ROOT differs from the prof version by the exchange prof->debug in the qualifier string



