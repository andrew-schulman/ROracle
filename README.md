# ROracle 1.3, patched for Windows

This is a patched version of ROracle 1.3, forked from https://github.com/cran/ROracle. The patch fixes a build error in Windows, by adding a missing file (ociver.h) into the configure script for Windows. For background on the bug, which is unfixed for 5 years as of November 2023, see https://stackoverflow.com/questions/52215350/roracle-package-installation-failure.

To build ROracle from this repo instead of from CRAN, just run

    devtools::install_github('andrew-schulman/ROracle')
