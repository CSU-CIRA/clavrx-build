FROM clavrx-deps:latest

ADD clavrx-dev /install_clavrx/clavrx-dev/

ENV hdf4_gcc /install_clavrx/lib/hdf4/
ENV hdf5_gcc /install_clavrx/lib/hdf5/
ENV netcdf_gcc /install_clavrx/lib/netcdf4/

# Move the include and src (libs end up in src) dirs somewhere more useful
# and out of the workdir so we can delete that from the image
# I could not get the CLAVR-x build to work with the Himawari library
# Lots of undefined reference to `operator delete(void*, unsigned long)' errors
# and undefined reference to `std::__throw_out_of_range_fmt(char const*, ...)' errors
# even if I add devtoolset-7 include paths to the libhimawari makefile and make depend exits without error
#ENV LIBHIM_PATH /workdir/libhimawari/

# Move the bin, lib, and include dirs somewhere more useful 
# and out of the workdir so we can delete that from the image
ENV RTTOV_PATH /workdir/RTTOV123/

ENV FC gfortran
ENV ARCH gfortran
ENV FFLAGS -g
ENV fflags -g

WORKDIR /install_clavrx/clavrx-dev

#RUN ./configure -LIBHIM_GCC=$LIBHIM_PATH --rttov_path=$RTTOV_PATH -hdf4_gcc=$hdf4_gcc -hdf5_gcc=$hdf5_gcc -netcdf_gcc=$netcdf_gcc
RUN source scl_source enable devtoolset-7 && \
./configure --rttov_path=$RTTOV_PATH -hdf4_gcc=$hdf4_gcc -hdf5_gcc=$hdf5_gcc -netcdf_gcc=$netcdf_gcc && \
cd main_src && make all_plus

