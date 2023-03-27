## Overview
Builds [CLAVR-x source code](https://gitlab.ssec.wisc.edu/clavrx/clavrx-dev.git) on top of the CLAVR-x dependencies image

## Run instructions
### Set up
CLAVR-x is intended to be built in a Docker image described by the Dockerfile in the dependencies folder named `clavrx-deps:rockylinux8.7`. If the dependencies image is named differently, 
the Dockerfile will need to be modified to account for this. 
The Dockerfile also assumes that the [CLAVR-x source code](https://gitlab.ssec.wisc.edu/clavrx/clavrx-dev.git) is in the same directory as the Dockerfile.
<br>
To get the code and set it up:
`git clone https://gitlab.ssec.wisc.edu/clavrx/clavrx-dev.git CLAVRx`
`cd CLAVRx`
`git checkout develop`

### Building the Image
Build the CLAVR-X image using the command `docker build -t clavrx-src:develop --network host .` Note the `.` assumes you are working in the directory that
contains the Dockerfile. To provide an alternate path, trade the period
out for `-f /path/to/the/Dockerfile`

### Creating a container from the image
Although the default Docker behavior will create a container that runs
as root, it is best practice to declare your own user when you create
the container to avoid messy security issues. For compatability with
the host machine, you can use your user and preferred group ids in the
container, or if compatability is not an issue, you may simply create a new user:group identification for the container. To get your user and group id
on the host (provided that you are working in a linux-like environment), use
`id`.

To create and run a container from the image, use something like
`docker run -it --name container_name_of_your_choice -u uid:gid -v /path/to/data/on/host:/path/to/data/in/the/container eco1280_convert:1.0`,
adding -v flags before the image name as necessary to provide any data mounts
needed for the code to be able to access the necessary input data.
Again, the `--name` is optional but makes the container easily locatable. For example, `docker run -it --name clavrx-test-hqc -v /home/hcronk/GEO_runs:/home/hcronk/GEO_runs -v /mnt/data1/clavrx_ancil_data:/mnt/data1/clavrx_ancil_data -v /mnt/jpssnas2/clavrx_ancil_data/dynamic:/mnt/data1/clavrx_ancil_data/dynamic clavrx-src`


### Entering the container
The `-it` flag in the `docker build` command will start an interactive
session within the container, where you will be dropped in the
`/ECO1280_int_scripts` directory where the conversion scripts are located.
If the container is stopped (you can check by running `docker ps`),
start it by running, for example, `docker start clavrx-test-hqc` and then enter it
using `docker exec -it clavrx-test-hqc /bin/bash`.

### Running the lat/lon converter
The CLAVR-x executable will be in `/install_clavrx/clavrx-dev/clavrx_bin`. A sample call looks like:
`./clavrxorb -file_list $testdir/RadF/clavrxorb_file_list -default $testdir/clavrxorb_default_options -level2_list $testdir/level2_list_ML`
