# ROracle 1.3, patched for Windows

This is a patched version of ROracle 1.3, forked from https://github.com/cran/ROracle. It fixes two build errors in Windows:

1. Adds a missing file (ociver.h) into the Windows configure script. For background on the bug, which is unfixed upstream for 5 years as of November 2023, see https://stackoverflow.com/questions/52215350/roracle-package-installation-failure.

2. Quotes the pathname to the Oracle client, avoiding build failures when the pathname contains spaces.

## Installation in Windows

To build and install ROracle in Windows from this repo:

1. Install the [Oracle client](https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html) on your PC. You need at least the Basic and SDK packages.

2. Set the ORACLE_HOME environment variable to the root directory of wherever you installed the Oracle client. (In Windows Explorer, go to Computer or This PC > Properties > Advanced System Settings > Environment Variables.)

3. Install [RTools](https://cran.r-project.org/bin/windows/Rtools).

4. Install the `devtools` package in R.

5. Set environment variables in R:
   ```
   Oracle_home <- Sys.getenv("ORACLE_HOME")
   Sys.setenv(
     OCI_LIB64 = Oracle_home,
     OCI_LIB = Oracle_home,
     OCI_INC = paste0(Oracle_home, "/sdk/include"),
     PATH = paste0(Sys.getenv("PATH"), ";", Oracle_home, ";", R.home(), "/bin/x64")
   )
   ```

6. You can now build and install the package from this repo's source. Run
   ```
   options(configure.args = paste0("--with-oci-lib=", Oracle_home, " --with-oci-inc=", Oracle_home, "/sdk/include"))
   devtools::install_github("andrew-schulman/ROracle")
   ```

See also the INSTALL file in the package source.

## Using ROracle in Windows

At run time, before you can load ROracle in Windows, you have to update the PATH environment variable to include the R and Oracle home directories:

    Sys.setenv(
	  PATH = paste0(Sys.getenv("PATH"), ";", Sys.getenv("ORACLE_HOME"), ";", R.home(), "/bin/x64")
	)

If you don't do that, then when you try to use ROracle, for example by calling `dbConnect(ROracle::Oracle(), ...)`, you'll get an error like this one:

    Error: package or namespace load failed for ‘ROracle’ in inDL(x, as.logical(local), as.logical(now), ...):
     unable to load shared object 'C:/Users/aschulma/Software/R/win-library/4.3/ROracle/libs/x64/ROracle.dll':
      LoadLibrary failure:  The specified module could not be found.
