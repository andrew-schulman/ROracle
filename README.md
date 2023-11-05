# ROracle 1.3, patched for Windows

This is a patched version of ROracle 1.3, forked from https://github.com/cran/ROracle. It fixes two build errors in Windows:

1. Adds a missing file (ociver.h) into the Windows configure script. For background on the bug, which is unfixed for 5 years as of November 2023, see https://stackoverflow.com/questions/52215350/roracle-package-installation-failure.

2. Quotes the pathname to the Oracle client, avoiding build failures when the pathname contains spaces.

To build ROracle from this repo instead of from CRAN, just run

    devtools::install_github('andrew-schulman/ROracle')
