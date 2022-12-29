## Overview

Builds the necessary and optional dependencies for running [CLAVR-x](http://cimss.ssec.wisc.edu/clavr/documentation.html)

## Run instructions
### Set up
CLAVR-x is intended to be built in an environment described by the Dockerfile in this folder. In order to build the image, Docker must be installed on the host system. The docker build also assumes that the source code for RTTOV and libHimawari are in subdirectories of this Dockerfile (libhimawari and RTTOV123, respectively).

### Building the Image
Build the CLAVR-X dependencies image using the command `docker build -t clavrx-deps .` Note the `.` assumes you are working in the directory that
contains the Dockerfile. To provide an alternate path, trade the period
out for `-f /path/to/the/Dockerfile`
