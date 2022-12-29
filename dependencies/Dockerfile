FROM centos:7

RUN yum install -y epel-release centos-release-scl-rh
RUN yum install -y devtoolset-7-gcc* make libtirpc-devel byacc flex libjpeg-turbo-devel zlib-devel libcurl-devel perl perl-Data-Dumper

RUN mkdir -p /install_clavrx/lib

WORKDIR /workdir

ADD https://support.hdfgroup.org/ftp/HDF/releases/HDF4.2.14/src/hdf-4.2.14.tar.gz .
RUN tar xf hdf-4.2.14.tar.gz && cd hdf-4.2.14 && source scl_source enable devtoolset-7 && \
./configure LIBS=-ltirpc CPPFLAGS=-I/usr/include/tirpc --disable-netcdf --prefix=/install_clavrx/lib/hdf4 && \
make && make install

ADD https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.8/hdf5-1.8.21/src/hdf5-1.8.21.tar.gz .
RUN tar xf hdf5-1.8.21.tar.gz && cd hdf5-1.8.21 && source scl_source enable devtoolset-7 && \
./configure --enable-fortran --enable-fortran2003 --enable-cxx --enable-shared --enable-hl --prefix=/install_clavrx/lib/hdf5 && \
make && make install

ADD https://github.com/Unidata/netcdf-c/archive/refs/tags/v4.7.0.tar.gz .
RUN tar xf v4.7.0.tar.gz && cd netcdf-c-4.7.0 && source scl_source enable devtoolset-7 && \
./configure --prefix=/install_clavrx/lib/netcdf4 LDFLAGS='-L/install_clavrx/lib/hdf5/lib' CPPFLAGS='-I/install_clavrx/lib/hdf5/include' && \
make && make install

ENV NCDIR /install_clavrx/lib/netcdf4
ENV NETCDF /install_clavrx/lib/netcdf4
ENV NETCDF4 /install_clavrx/lib/netcdf4
ENV NFDIR /install_clavrx/lib/netcdf4
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/install_clavrx/lib/hdf4/lib:/install_clavrx/lib/hdf5/lib:/install_clavrx/lib/netcdf4/lib

ADD https://downloads.unidata.ucar.edu/netcdf-fortran/4.4.4/netcdf-fortran-4.4.4.tar.gz .
RUN tar xf netcdf-fortran-4.4.4.tar.gz && cd netcdf-fortran-4.4.4 && source scl_source enable devtoolset-7 && \
./configure --prefix=/install_clavrx/lib/netcdf4 LDFLAGS='-L/install_clavrx/lib/hdf5/lib -L/install_clavrx/lib/netcdf4/lib' CPPFLAGS='-I/install_clavrx/lib/hdf5/include -I/install_clavrx/lib/netcdf4/include' && \
make && make install

ADD RTTOV123 RTTOV123/
RUN source scl_source enable devtoolset-7 && cd RTTOV123/src && /workdir/RTTOV123/build/rttov_compile.sh

ADD libhimawari libhimawari/
RUN source scl_source enable devtoolset-7 && cd libhimawari/src && make

