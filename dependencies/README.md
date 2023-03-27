## Overview

Builds the necessary and optional dependencies for running [CLAVR-x](http://cimss.ssec.wisc.edu/clavr/documentation.html)

## Run instructions
### Set up
CLAVR-x is intended to be built in an environment described by the Dockerfile in this folder. In order to build the image, Docker must be installed on the host system. The docker build also assumes that the source code for RTTOV are in a subdirectory of this Dockerfile.
<br>
After a free registration process, the RTTOV source code and 
ancillary files can be downloaded from 
https://nwp-saf.eumetsat.int/site/software/rttov/download/
The next set of directives assume you have RTTOV untarred
in your build directory where the Dockerfile is because there are modifications
that need to be made to the source code before compiling.
Note that this tarball unpacks everything into your CWD by default,
so be sure to use a `-C` with your tar!
(e.g., `mkdir rttov132 && tar xf rttov132.tar.xz -C ./rttov132`)

### Building the Image
Build the CLAVR-X dependencies image using the command `docker build -t clavrx-deps:rockylinux --network host .` Note the `.` assumes you are working in the directory that
contains the Dockerfile. To provide an alternate path, trade the period
out for `-f /path/to/the/Dockerfile`
