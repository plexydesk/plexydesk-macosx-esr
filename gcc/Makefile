LOC=/opt/dist/gcc-5.4.0/i686
CFLAGS='-mmacosx-version-min=10.4'

all: sudo prerequistes gcc

clean:
	@echo TODO

sudo:
	@echo Authentication is needed for this build
	sudo whoami

gcc:
	wget -q -c https://ftp.gnu.org/gnu/gcc/gcc-5.4.0/gcc-5.4.0.tar.gz
	tar xfz gcc-5.4.0.tar.gz
	(cd gcc-5.4.0 && mkdir -p build && cd build && ABI=32 MACOSX_DEPLOYMENT_TARGET=10.4  CFLAGS=${CFLAGS} ../configure -q --enable-languages=obj-c++,objc,c,c++ --prefix=${LOC} --enable-checking=release --with-system-zlib --enable-libstdcxx-time=yes --enable-stage1-checking --enable-plugin --disable-nls  --enable-lto --disable-werror --with-gmp=${LOC} --with-mpfr=${LOC} --with-mpc=${LOC} --with-isl=${LOC} --program-suffix=-5.4 && make -s all-gcc && make -s  all-target-libgcc && sudo make install-gcc && sudo make install-target-libgcc && sudo make && sudo make all-target-libstdc++-v3 && sudo make install-target-libstdc++-v3)

bootstrap: gmp mpfr mpc isl

gmp:
	wget -q -c https://gmplib.org/download/gmp/gmp-6.1.2.tar.bz2 
	tar jxf gmp-6.1.2.tar.bz2 
	(cd gmp-6.1.2 && mkdir -p build && cd build && MACOSX_DEPLOYMENT_TARGET=10.4  CFLAGS=${CFLAGS} ../configure  ABI=32 -q --prefix=${LOC} --enable-cxx --enable-multilib && make -s && sudo make install)

mpfr:
	wget -c -q http://www.mpfr.org/mpfr-3.1.5/mpfr-3.1.5.tar.gz
	tar xfz mpfr-3.1.5.tar.gz
	(cd mpfr-3.1.5 && mkdir -p build && cd build && MACOSX_DEPLOYMENT_TARGET=10.4  CFLAGS=${CFLAGS} ../configure -q --prefix=${LOC}  --with-gmp=${LOC} && make -s && sudo make install)

mpc:
	wget -c  -q http://www.multiprecision.org/mpc/download/mpc-1.0.3.tar.gz
	tar xfz mpc-1.0.3.tar.gz
	(cd mpc-1.0.3 && mkdir -p build && cd build && MACOSX_DEPLOYMENT_TARGET=10.4  CFLAGS=${CFLAGS} ../configure -q  --prefix=${LOC} --with-gmp=${LOC} --with-mpfr=${LOC} && make -s && sudo make install)


isl:
	wget -q -c ftp://gcc.gnu.org/pub/gcc/infrastructure/isl-0.14.tar.bz2
	tar xfj isl-0.14.tar.bz2
	(cd  isl-0.14 && mkdir -p build && cd build && MACOSX_DEPLOYMENT_TARGET=10.4  CFLAGS=${CFLAGS} ../configure -q --prefix=${LOC} --with-sysroot=/Developer/SDKs/MacOSX10.4u.sdk/ --with-gmp-prefix=${LOC} && make -s && sudo make install)
