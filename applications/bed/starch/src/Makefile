C       = gcc
CPP     = g++
AR      = ar

ifneq ($(wildcard .forcestatic),)
	SFLAGS = -static -s
else
	SFLAGS =
endif

HEAD	                  = ../../../..
INTERFACES                = $(HEAD)/interfaces
MAIN	                  = ${INTERFACES}/general-headers
MAINAPPDIR                = ../..
PARTY3                    = $(HEAD)/third-party
CFLAGS                    = -D__STDC_CONSTANT_MACROS -D_FILE_OFFSET_BITS=64 -D_LARGEFILE64_SOURCE=1 -DUSE_ZLIB -DUSE_BZLIB -O2 -Wformat -Wall -Wextra -Wswitch-enum -std=c99 ${SFLAGS}
CPPFLAGS                  = -D__STDC_CONSTANT_MACROS -D_FILE_OFFSET_BITS=64 -D_LARGEFILE64_SOURCE=1 -DUSE_ZLIB -DUSE_BZLIB -O2 -Wformat -Wall -Wextra -Wswitch-enum -std=c++11 ${SFLAGS}
CDFLAGS                   = -D__STDC_CONSTANT_MACROS -D_FILE_OFFSET_BITS=64 -D_LARGEFILE64_SOURCE=1 -DUSE_ZLIB -DUSE_BZLIB -O0 -g -Wformat -Wall -Wextra -Wswitch-enum -std=c99 -fgnu89-inline -DDEBUG=1 -static
CPPDFLAGS                 = -D__STDC_CONSTANT_MACROS -D_FILE_OFFSET_BITS=64 -D_LARGEFILE64_SOURCE=1 -DUSE_ZLIB -DUSE_BZLIB -O0 -g -Wformat -Wall -Wextra -Wswitch-enum -std=c++11 -DDEBUG=1 -static
CGFLAGS                   = -D__STDC_CONSTANT_MACROS -D_FILE_OFFSET_BITS=64 -D_LARGEFILE64_SOURCE=1 -DUSE_ZLIB -DUSE_BZLIB -O -Wformat -Wall -Wextra -Wswitch-enum -std=c99 -fgnu89-inline -DDEBUG=1 -static -pg
CPPGFLAGS                 = -D__STDC_CONSTANT_MACROS -D_FILE_OFFSET_BITS=64 -D_LARGEFILE64_SOURCE=1 -DUSE_ZLIB -DUSE_BZLIB -O -Wformat -Wall -Wextra -Wswitch-enum -std=c++11 -DDEBUG=1 -static -pg
BIN                       = ../bin
THISDIR	                  = ${shell pwd}
LIBSTARCH                 = libstarch.a
LIBSTARCHDEBUG            = libstarch_debug.a
LIBSTARCHGPROF            = libstarch_gprof.a
LIBJANSSON                = libjansson.a
LIBBZIP2                  = libbz2.a
LIBZLIB                   = libz.a
LOCALSTARCHLIBDIR         = ../lib
LOCALSTARCHLIBPATH        = ${LOCALSTARCHLIBDIR}/${LIBSTARCH}
LOCALSTARCHLIBDEBUGPATH   = ${LOCALSTARCHLIBDIR}/${LIBSTARCHDEBUG}
LOCALSTARCHLIBGPROFPATH   = ${LOCALSTARCHLIBDIR}/${LIBSTARCHGPROF}
LOCALJANSSONDIR           = ${THISDIR}/${PARTY3}/jansson
LOCALJANSSONLIBDIR        = ${LOCALJANSSONDIR}/lib
LOCALJANSSONLIBPATH       = ${LOCALJANSSONLIBDIR}/${LIBJANSSON}
LOCALJANSSONINCDIR        = ${LOCALJANSSONDIR}/include
LOCALBZIP2DIR             = ${THISDIR}/${PARTY3}/bzip2
LOCALBZIP2LIBDIR          = ${LOCALBZIP2DIR}
LOCALBZIP2LIBPATH         = ${LOCALBZIP2LIBDIR}/${LIBBZIP2}
LOCALBZIP2INCDIR          = ${LOCALBZIP2DIR}
LOCALZLIBDIR              = ${THISDIR}/${PARTY3}/zlib
LOCALZLIBLIBDIR           = ${LOCALZLIBDIR}
LOCALZLIBLIBPATH          = ${LOCALZLIBLIBDIR}/${LIBZLIB}
LOCALZLIBINCDIR           = ${LOCALZLIBDIR}
OBJDIR                    = ${INTERFACES}/src/data/starch
LOCALOBJDIR                 = objects
PLATFORM                  = ${shell uname}
ARCH_VERSION              = v2.0
BIN_VERSION               = v2.4
TEST                      = ../test
TEST_LINUX_BINDIR         = ${TEST}/binaries/linux/${ARCH_VERSION}/bin
TEST_OSX_BINDIR           = ${TEST}/binaries/osx/${ARCH_VERSION}/bin

.PHONY: starchcluster

all: clean_force_flags dependencies starchLibrary starch unstarch starchcat starchcluster
	rm -rf *~

dependencies: jansson bzip2 zlib
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPFLAGS} -c ${OBJDIR}/starchConstants.c -o ${LOCALOBJDIR}/starchConstants.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} -c ${OBJDIR}/starchMetadataHelpers.c -o  ${LOCALOBJDIR}/starchMetadataHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} -c ${OBJDIR}/unstarchHelpers.c -o  ${LOCALOBJDIR}/unstarchHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} -c ${OBJDIR}/starchHelpers.c -o  ${LOCALOBJDIR}/starchHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} -c ${OBJDIR}/starchFileHelpers.c -o  ${LOCALOBJDIR}/starchFileHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} -c ${OBJDIR}/starchSha1Digest.c -o  ${LOCALOBJDIR}/starchSha1Digest.o -iquote${MAIN} -iquote${PARTY3} -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} -c ${OBJDIR}/starchBase64Coding.c -o  ${LOCALOBJDIR}/starchBase64Coding.o -iquote${MAIN} -iquote${PARTY3} -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}

debug: clean_force_flags dependencies_debug starchLibrary_debug starch_debug unstarch_debug starchcat_debug starchcluster
	rm -rf *~

dependencies_debug: jansson bzip2 zlib
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPDFLAGS} -c ${OBJDIR}/starchConstants.c -o ${LOCALOBJDIR}/starchConstants.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} -c ${OBJDIR}/unstarchHelpers.c -o  ${LOCALOBJDIR}/unstarchHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} -c ${OBJDIR}/starchHelpers.c -o  ${LOCALOBJDIR}/starchHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} -c ${OBJDIR}/starchMetadataHelpers.c -o  ${LOCALOBJDIR}/starchMetadataHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} -c ${OBJDIR}/starchFileHelpers.c -o  ${LOCALOBJDIR}/starchFileHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} -c ${OBJDIR}/starchSha1Digest.c -o  ${LOCALOBJDIR}/starchSha1Digest.o -iquote${MAIN} -iquote${PARTY3} -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} -c ${OBJDIR}/starchBase64Coding.c -o  ${LOCALOBJDIR}/starchBase64Coding.o -iquote${MAIN} -iquote${PARTY3} -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}

gprof: clean_force_flags dependencies_gprof starchLibrary_gprof starch_gprof unstarch_gprof starchcat_gprof starchcluster
	rm -rf *~

dependencies_gprof: jansson bzip2 zlib
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPGFLAGS} -c ${OBJDIR}/starchConstants.c -o ${LOCALOBJDIR}/starchConstants.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPGFLAGS} -c ${OBJDIR}/unstarchHelpers.c -o  ${LOCALOBJDIR}/unstarchHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPGFLAGS} -c ${OBJDIR}/starchHelpers.c -o  ${LOCALOBJDIR}/starchHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPGFLAGS} -c ${OBJDIR}/starchMetadataHelpers.c -o  ${LOCALOBJDIR}/starchMetadataHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPGFLAGS} -c ${OBJDIR}/starchFileHelpers.c -o  ${LOCALOBJDIR}/starchFileHelpers.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPGFLAGS} -c ${OBJDIR}/starchSha1Digest.c -o  ${LOCALOBJDIR}/starchSha1Digest.o -iquote${MAIN} -iquote${PARTY3} -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPGFLAGS} -c ${OBJDIR}/starchBase64Coding.c -o  ${LOCALOBJDIR}/starchBase64Coding.o -iquote${MAIN} -iquote${PARTY3} -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}

clean_force_flags:
ifneq ($(wildcard .forcestatic),)
	rm -rf .forcestatic
endif

jansson:
	test -d ${LOCALJANSSONDIR} || { cd ${HEAD} && make jansson_support_c && cd ${THISDIR}; }
	cd ${LOCALJANSSONDIR} && ${LOCALJANSSONDIR}/configure --prefix=${LOCALJANSSONDIR} && make clean && make && make install && cd ${THISDIR}

bzip2:
	test -d ${LOCALBZIP2DIR} || { cd ${HEAD} && make bzip2_support_c && cd ${THISDIR}; }
	cd ${LOCALBZIP2DIR} && make libbz2.a && cd ${THISDIR}

zlib:
	test -d ${LOCALZLIBDIR} || { cd ${HEAD} && make zlib_support_c && cd ${THISDIR}; }
	cd ${LOCALZLIBDIR} && ${LOCALZLIBDIR}/configure --static && make && cd ${THISDIR}

starchLibrary: dependencies
	mkdir -p ${LOCALSTARCHLIBDIR}
	${AR} rcs ${LOCALSTARCHLIBPATH} ${LOCALOBJDIR}/starchConstants.o  ${LOCALOBJDIR}/unstarchHelpers.o  ${LOCALOBJDIR}/starchHelpers.o  ${LOCALOBJDIR}/starchMetadataHelpers.o  ${LOCALOBJDIR}/starchFileHelpers.o ${LOCALOBJDIR}/starchSha1Digest.o ${LOCALOBJDIR}/starchBase64Coding.o

starchLibrary_debug: dependencies_debug
	mkdir -p ${LOCALSTARCHLIBDIR}
	${AR} rcs ${LOCALSTARCHLIBDEBUGPATH} ${LOCALOBJDIR}/starchConstants.o  ${LOCALOBJDIR}/unstarchHelpers.o  ${LOCALOBJDIR}/starchHelpers.o  ${LOCALOBJDIR}/starchMetadataHelpers.o  ${LOCALOBJDIR}/starchFileHelpers.o ${LOCALOBJDIR}/starchSha1Digest.o ${LOCALOBJDIR}/starchBase64Coding.o

starchLibrary_gprof: dependencies_gprof
	mkdir -p ${LOCALSTARCHLIBDIR}
	${AR} rcs ${LOCALSTARCHLIBGPROFPATH} ${LOCALOBJDIR}/starchConstants.o  ${LOCALOBJDIR}/unstarchHelpers.o  ${LOCALOBJDIR}/starchHelpers.o  ${LOCALOBJDIR}/starchMetadataHelpers.o  ${LOCALOBJDIR}/starchFileHelpers.o ${LOCALOBJDIR}/starchSha1Digest.o ${LOCALOBJDIR}/starchBase64Coding.o

starch: starchLibrary
	mkdir -p $(BIN)
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPFLAGS} -c starch.c -o $(LOCALOBJDIR)/starch.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} $(LOCALOBJDIR)/starch.o -o ${BIN}/starch ${LOCALSTARCHLIBPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}
	rm -rf *~

starch_debug: starchLibrary_debug
	mkdir -p $(BIN)
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPDFLAGS} -c starch.c -o $(LOCALOBJDIR)/debug.starch.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} $(LOCALOBJDIR)/debug.starch.o -o ${BIN}/debug.starch ${LOCALSTARCHLIBDEBUGPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}
	rm -rf *~

starch_gprof: starchLibrary_gprof
	mkdir -p $(BIN)
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPDFLAGS} -c starch.c -o $(LOCALOBJDIR)/gprof.starch.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} $(LOCALOBJDIR)/gprof.starch.o -o ${BIN}/gprof.starch ${LOCALSTARCHLIBGPROFPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}
	rm -rf *~

unstarch: starchLibrary
	mkdir -p $(BIN)
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPFLAGS} -c unstarch.c -o $(LOCALOBJDIR)/unstarch.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} $(LOCALOBJDIR)/unstarch.o -o ${BIN}/unstarch ${LOCALSTARCHLIBPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}
	rm -rf *~

unstarch_debug: starchLibrary_debug
	mkdir -p $(BIN)
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPDFLAGS} -c unstarch.c -o $(LOCALOBJDIR)/debug.unstarch.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} $(LOCALOBJDIR)/debug.unstarch.o -o ${BIN}/debug.unstarch ${LOCALSTARCHLIBDEBUGPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}
	rm -rf *~

unstarch_gprof: starchLibrary_gprof
	mkdir -p $(BIN)
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPGFLAGS} -c unstarch.c -o $(LOCALOBJDIR)/gprof.unstarch.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPGFLAGS} $(LOCALOBJDIR)/gprof.unstarch.o -o ${BIN}/gprof.unstarch ${LOCALSTARCHLIBGPROFPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}
	rm -rf *~

starchcluster: starchcat
	mkdir -p ${BIN} && touch starchcluster && cp starchcluster ${BIN}
	mkdir -p ${BIN} && touch starchcluster.gnu_parallel && cp starchcluster.gnu_parallel ${BIN}

starchcat: starchLibrary
	mkdir -p ${BIN}
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPFLAGS} -c starchcat.c -o $(LOCALOBJDIR)/starchcat.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPFLAGS} $(LOCALOBJDIR)/starchcat.o -o ${BIN}/starchcat ${LOCALSTARCHLIBPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}

starchcat_debug: starchLibrary_debug
	mkdir -p ${BIN}
	mkdir -p $(LOCALOBJDIR)
	${CPP} ${CPPDFLAGS} -c starchcat.c -o $(LOCALOBJDIR)/debug.starchcat.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPDFLAGS} $(LOCALOBJDIR)/debug.starchcat.o -o ${BIN}/debug.starchcat ${LOCALSTARCHLIBDEBUGPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}

starchcat_gprof: starchLibrary_gprof
	mkdir -p ${BIN}
	mkdir -p ${LOCALOBJDIR}
	${CPP} ${CPPGFLAGS} -c starchcat.c -o $(LOCALOBJDIR)/gprof.starchcat.o -iquote${MAIN} -iquote$(PARTY3) -I${LOCALJANSSONINCDIR} -I${LOCALBZIP2INCDIR} -I${LOCALZLIBINCDIR}
	${CPP} ${CPPGFLAGS} $(LOCALOBJDIR)/gprof.starchcat.o -o ${BIN}/gprof.starchcat ${LOCALSTARCHLIBGPROFPATH} ${LOCALJANSSONLIBPATH} ${LOCALBZIP2LIBPATH} ${LOCALZLIBLIBPATH}

test: starch unstarch starchcat
ifeq (${PLATFORM},Linux)
	cp ${BIN}/starch ${TEST_LINUX_BINDIR}/starch
	cp ${BIN}/unstarch ${TEST_LINUX_BINDIR}/unstarch
	cp ${BIN}/starchcat ${TEST_LINUX_BINDIR}/starchcat
endif
ifeq (${PLATFORM},Darwin)
	cp ${BIN}/starch ${TEST_OSX_BINDIR}/starch
	cp ${BIN}/unstarch ${TEST_OSX_BINDIR}/unstarch
	cp ${BIN}/starchcat ${TEST_OSX_BINDIR}/starchcat
endif
	make -C ${TEST} all

clean:
	rm -rf $(LOCALSTARCHLIBPATH) ${LOCALSTARCHLIBDEBUGPATH} *~ ${BIN}/*
	rm -rf ${LOCALOBJDIR}
	-test -d ${LOCALJANSSONDIR} && { cd ${LOCALJANSSONDIR} && make clean && cd ${THISDIR}; }
	-test -d ${LOCALBZIP2DIR} && { cd ${LOCALBZIP2DIR} && make clean && cd ${THISDIR}; }
	-test -d ${LOCALZLIBDIR} && { cd ${LOCALZLIBDIR} && make -f Makefile.in clean && cd ${THISDIR}; }
