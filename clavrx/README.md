## Overview
Builds [CLAVR-x source code](https://gitlab.ssec.wisc.edu/clavrx/clavrx-dev.git) on top of the CLAVR-x dependencies image

## Run instructions
### Set up
CLAVR-x is intended to be built in an environment described by the Dockerfile in the dependencies folder named `clavrx-deps`. If the dependencies image is named differently, the Dockerfile will need to be modified to account for this. The Dockerfile also assumes that the [CLAVR-x source code](https://gitlab.ssec.wisc.edu/clavrx/clavrx-dev.git) is in the same directory as the Dockerfile.

### Building the Image
Build the CLAVR-X image using the command `docker build -t clavrx-src .` Note the `.` assumes you are working in the directory that
contains the Dockerfile. To provide an alternate path, trade the period
out for `-f /path/to/the/Dockerfile`
