FROM rockylinux:8.7

RUN yum install -y epel-release
RUN yum install -y gcc gcc-gfortran gcc-c++ make libtirpc-devel byacc flex git libjpeg-turbo-devel zlib-devel libcurl-devel perl perl-Data-Dumper libxml2-devel

RUN mkdir -p /install_clavrx/lib

WORKDIR /workdir

ADD https://support.hdfgroup.org/ftp/HDF/releases/HDF4.2.15/src/hdf-4.2.15.tar.gz .
RUN tar xf hdf-4.2.15.tar.gz && cd hdf-4.2.15 && \
./configure LIBS=-ltirpc CPPFLAGS=-I/usr/include/tirpc --disable-netcdf --prefix=/install_clavrx/lib/hdf4 && \
make && make install

ADD https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.9/src/hdf5-1.10.9.tar.gz .
RUN tar xf hdf5-1.10.9.tar.gz && cd hdf5-1.10.9 && \
./configure --enable-fortran --enable-cxx --enable-shared --enable-hl --prefix=/install_clavrx/lib/hdf5 && \
make && make install

ADD https://github.com/Unidata/netcdf-c/archive/refs/tags/v4.9.0.tar.gz .
RUN tar xf v4.9.0.tar.gz && cd netcdf-c-4.9.0 && \
./configure --prefix=/install_clavrx/lib/netcdf4 LDFLAGS='-L/install_clavrx/lib/hdf5/lib' CPPFLAGS='-I/install_clavrx/lib/hdf5/include' && \
make && make install

ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/install_clavrx/lib/netcdf4/lib:/install_clavrx/lib/hdf4/lib:/install_clavrx/lib/hdf5/lib

ADD https://github.com/Unidata/netcdf-fortran/archive/refs/tags/v4.6.0.tar.gz .
RUN tar xf v4.6.0.tar.gz && cd netcdf-fortran-4.6.0 && \
./configure --prefix=/install_clavrx/lib/netcdf4 LDFLAGS='-L/install_clavrx/lib/hdf5/lib -L/install_clavrx/lib/netcdf4/lib' CPPFLAGS='-I/install_clavrx/lib/hdf5/include -I/install_clavrx/lib/netcdf4/include' && \
make && make install

RUN git clone https://gitlab.ssec.wisc.edu/rayg/himawari.git libHimawari && \
cd libHimawari/src && make

# After a free registration process, the RTTOV source code and 
# ancillary files can be downloaded from 
# https://nwp-saf.eumetsat.int/site/software/rttov/download/
# The next set of directives assume you have RTTOV untarred
# in your build directory where the Dockerfile is because there are modifications
# that need to be made to the source code before compiling.
# Note that this tarball unpacks everything into your CWD by default,
# so be sure to use a `-C` with your tar!
# (e.g., `mkdir rttov132 && tar xf rttov132.tar.xz -C ./rttov132`)

ADD rttov132 rttov132/
ADD rttov_compile.sh rttov132/build/rttov_compile.sh
RUN cd rttov132/src && /workdir/rttov132/build/rttov_compile.sh

