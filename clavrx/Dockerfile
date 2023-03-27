FROM clavrx-deps:rockylinux8.7

RUN dnf install -y python3.9 which
# Need to create a simlink instead of an alias because 
# the alias only exists for that intermediate layer in the image
RUN cd "$(dirname $(which python3))" && ln -s python3 python

WORKDIR /install_clavrx

# The next directive assumes that you have the CLAVR-x source
# code cloned into directory where the Dockerfile is and 
# that you are working on the develop branch (main
# doesn't have quickstart capability yet).
# To get the code and set it up:
# `git clone https://gitlab.ssec.wisc.edu/clavrx/clavrx-dev.git CLAVRx`
# `cd CLAVRx`
# `git checkout develop`

ADD CLAVRx CLAVRx/

ADD user_change_me-rockylinux-docker.cfg CLAVRx/build/env_settings/user_change_me.cfg

RUN cd CLAVRx/build && ./admin clean ALL && ./admin build

ENV PATH $PATH:/install_clavrx/CLAVRx/run/bin

