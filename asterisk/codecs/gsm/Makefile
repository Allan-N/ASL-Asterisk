# Copyright 1992-1996 by Jutta Degener and Carsten Bormann, Technische
# Universitaet Berlin.  See the accompanying file "COPYRIGHT" for
# details.  THERE IS ABSOLUTELY NO WARRANTY FOR THIS SOFTWARE.

# Machine- or installation dependent flags you should configure to port

SASR	= -DSASR
######### Define SASR if >> is a signed arithmetic shift (-1 >> 1 == -1)

#MULHACK = -DUSE_FLOAT_MUL
######### Define this if your host multiplies floats faster than integers,
######### e.g. on a SPARCstation.

#FAST	= -DFAST
######### Define together with USE_FLOAT_MUL to enable the GSM library's
######### approximation option for incorrect, but good-enough results.

# LTP_CUT	= -DLTP_CUT
LTP_CUT	=
######### Define to enable the GSM library's long-term correlation 
######### approximation option---faster, but worse; works for
######### both integer and floating point multiplications.
######### This flag is still in the experimental stage.

WAV49	= -DWAV49
#WAV49	=
######### Define to enable the GSM library's option to pack GSM frames 
######### in the style used by the WAV #49 format.  If you want to write
######### a tool that produces .WAV files which contain GSM-encoded data,
######### define this, and read about the GSM_OPT_WAV49 option in the
######### manual page on gsm_option(3).

#K6OPT	= -DK6OPT
#K6OPT	=
######### Define to enable MMXTM optimizations for x86 architecture CPU's
######### which support MMX instructions.  This should be newer pentiums,
######### ppro's, etc, as well as the AMD K6 and K7.  The compile will
######### probably require gcc. 

ifeq (, $(findstring $(OSARCH) , Darwin SunOS ))
ifeq (, $(findstring $(PROC) , x86_64 amd64 aarch64 ultrasparc sparc64 arm armv5b armeb hppa2.0 ppc powerpc ppc64 ia64 s390 bfin mipsel mips))
ifeq (, $(findstring $(shell uname -m) , ppc ppc64 alpha armv4l armv7l s390 ))
OPTIMIZE+=-march=$(PROC)
endif
endif
endif

#The problem with sparc is the best stuff is in newer versions of gcc (post 3.0) only.
#This works for even old (2.96) versions of gcc and provides a small boost either way.
#A ultrasparc cpu is really v9 but the stock debian stable 3.0 gcc doesn't support it.
#So we go lowest common available by gcc and go a step down, still a step up from
#the default as we now have a better instruction set to work with. - Belgarath
ifeq ($(PROC),ultrasparc)
OPTIMIZE+=-mcpu=v8 -mtune=$(PROC) -O3 
endif

PG =
#PG = -g -pg
######### Profiling flags.  If you don't know what that means, leave it blank.
 
# Choose a compiler.  The code works both with ANSI and K&R-C.
# Use -DNeedFunctionPrototypes to compile with, -UNeedFunctionPrototypes to
# compile without, function prototypes in the header files.
#
# You can use the -DSTUPID_COMPILER to circumvent some compilers'
# static limits regarding the number of subexpressions in a statement.

# CC		= cc
# CCFLAGS 	= -c -DSTUPID_COMPILER

# CC		= /usr/lang/acc
# CCFLAGS 	= -c -O

CCFLAGS 	+= -c -DNeedFunctionPrototypes=1 -funroll-loops $(OPTIMIZE)

# LD		= gcc
# LDFLAGS 	=


# If your compiler needs additional flags/libraries, regardless of
# the source compiled, configure them here.

# CCINC	= -I/usr/gnu/lib/gcc-2.1/gcc-lib/sparc-sun-sunos4.1.2/2.1/include
######### Includes needed by $(CC)

# LDINC	= -L/usr/gnu/lib/gcc-2.1/gcc-lib/sparc-sun-sunos4.1.2/2.1
######### Library paths needed by $(LD)

# LDLIB	= -lgcc
######### Additional libraries needed by $(LD)


# Where do you want to install libraries, binaries, a header file
# and the manual pages?
#
# Leave INSTALL_ROOT empty (or just don't execute "make install") to
# not install gsm and toast outside of this directory.

INSTALL_ROOT	=

# Where do you want to install the gsm library, header file, and manpages?
#
# Leave GSM_INSTALL_ROOT empty to not install the GSM library outside of
# this directory.

GSM_INSTALL_ROOT = $(INSTALL_ROOT)
GSM_INSTALL_LIB = $(GSM_INSTALL_ROOT)/lib
GSM_INSTALL_INC = $(GSM_INSTALL_ROOT)/inc
GSM_INSTALL_MAN = $(GSM_INSTALL_ROOT)/man/man3


# Where do you want to install the toast binaries and their manpage?
#
# Leave TOAST_INSTALL_ROOT empty to not install the toast binaries outside
# of this directory.

TOAST_INSTALL_ROOT	  = $(INSTALL_ROOT)
TOAST_INSTALL_BIN = $(TOAST_INSTALL_ROOT)/bin
TOAST_INSTALL_MAN = $(TOAST_INSTALL_ROOT)/man/man1

#  Other tools

SHELL		= /bin/sh
LN		= ln
BASENAME 	= basename
AR		= ar
ARFLAGS		= cr
RMFLAGS		= -f
FIND		= find
COMPRESS 	= compress
COMPRESSFLAGS 	= 
# RANLIB 	= true
RANLIB	 	= ranlib

#
#    You shouldn't have to configure below this line if you're porting.
# 


# Local Directories

ROOT	= .
ADDTST	= $(ROOT)/add-test
TST	= $(ROOT)/tst
MAN	= $(ROOT)/man
BIN	= $(ROOT)/bin
SRC	= $(ROOT)/src
LIB	= $(ROOT)/lib
TLS	= $(ROOT)/tls
INC	= $(ROOT)/inc

# Flags

DEBUG	= -DNDEBUG
######### Remove -DNDEBUG to enable assertions.

ASTCFLAGS += $(PG) $(CCFLAGS) $(SASR) $(DEBUG) $(MULHACK) $(FAST) \
	$(LTP_CUT) $(WAV49) $(K6OPT) $(CCINC) -I$(INC)
######### It's $(CC) $(CFLAGS)

LFLAGS	= $(PG) $(LDFLAGS) $(LDINC)
######### It's $(LD) $(LFLAGS)


# Targets

LIBGSM	= $(LIB)/libgsm.a
LIBGSMSO= $(LIB)/libgsm.so

TOAST	= $(BIN)/toast
UNTOAST	= $(BIN)/untoast
TCAT	= $(BIN)/tcat

# Headers

GSM_HEADERS =	$(INC)/gsm.h

HEADERS	=	$(INC)/proto.h		\
		$(INC)/unproto.h	\
		$(INC)/config.h		\
		$(INC)/private.h	\
		$(INC)/gsm.h		\
		$(INC)/toast.h		\
		$(TLS)/taste.h

# Sources

GSM_SOURCES =	$(SRC)/add.c		\
		$(SRC)/code.c		\
		$(SRC)/debug.c		\
		$(SRC)/decode.c		\
		$(SRC)/long_term.c	\
		$(SRC)/lpc.c		\
		$(SRC)/preprocess.c	\
		$(SRC)/rpe.c		\
		$(SRC)/gsm_destroy.c	\
		$(SRC)/gsm_decode.c	\
		$(SRC)/gsm_encode.c	\
		$(SRC)/gsm_explode.c	\
		$(SRC)/gsm_implode.c	\
		$(SRC)/gsm_create.c	\
		$(SRC)/gsm_print.c	\
		$(SRC)/gsm_option.c	\
		$(SRC)/short_term.c	\
		$(SRC)/table.c

# add k6-specific code only if not on a non-k6 hardware or proc.
# XXX Keep a space after each findstring argument
# XXX should merge with GSM_OBJECTS
ifeq ($(OSARCH),linux-gnu)
ifeq (, $(findstring $(PROC) , x86_64 amd64 aarch64 ultrasparc sparc64 arm armv5b armeb hppa2.0 ppc powerpc ppc64 ia64 s390 bfin mipsel mips))
ifeq (, $(findstring $(shell uname -m) , ppc ppc64 alpha armv4l armv7l s390 ))
GSM_SOURCES+= $(SRC)/k6opt.s
endif
endif
endif

TOAST_SOURCES = $(SRC)/toast.c 		\
		$(SRC)/toast_lin.c	\
		$(SRC)/toast_ulaw.c	\
		$(SRC)/toast_alaw.c	\
		$(SRC)/toast_audio.c

SOURCES	=	$(GSM_SOURCES)		\
		$(TOAST_SOURCES)	\
		$(ADDTST)/add_test.c	\
		$(TLS)/sour.c		\
		$(TLS)/ginger.c		\
		$(TLS)/sour1.dta	\
		$(TLS)/sour2.dta	\
		$(TLS)/bitter.c		\
		$(TLS)/bitter.dta	\
		$(TLS)/taste.c		\
		$(TLS)/sweet.c		\
		$(TST)/cod2lin.c	\
		$(TST)/cod2txt.c	\
		$(TST)/gsm2cod.c	\
		$(TST)/lin2cod.c	\
		$(TST)/lin2txt.c

# Object files

GSM_OBJECTS =	$(SRC)/add.o		\
		$(SRC)/code.o		\
		$(SRC)/debug.o		\
		$(SRC)/decode.o		\
		$(SRC)/long_term.o	\
		$(SRC)/lpc.o		\
		$(SRC)/preprocess.o	\
		$(SRC)/rpe.o		\
		$(SRC)/gsm_destroy.o	\
		$(SRC)/gsm_decode.o	\
		$(SRC)/gsm_encode.o	\
		$(SRC)/gsm_explode.o	\
		$(SRC)/gsm_implode.o	\
		$(SRC)/gsm_create.o	\
		$(SRC)/gsm_print.o	\
		$(SRC)/gsm_option.o	\
		$(SRC)/short_term.o	\
		$(SRC)/table.o

ifeq ($(OSARCH),linux-gnu)
ifeq (, $(findstring $(PROC) , x86_64 amd64 aarch64 ultrasparc sparc64 arm armv5b armeb hppa2.0 ppc powerpc ppc64 ia64 s390 bfin mipsel mips))
ifeq (, $(findstring $(shell uname -m) , ppc ppc64 alpha armv4l armv7l s390 ))
GSM_OBJECTS+= $(SRC)/k6opt.o
endif
endif
endif

TOAST_OBJECTS =	$(SRC)/toast.o 		\
		$(SRC)/toast_lin.o	\
		$(SRC)/toast_ulaw.o	\
		$(SRC)/toast_alaw.o	\
		$(SRC)/toast_audio.o

OBJECTS =	 $(GSM_OBJECTS) $(TOAST_OBJECTS)

# Manuals

GSM_MANUALS =	$(MAN)/gsm.3		\
		$(MAN)/gsm_explode.3	\
		$(MAN)/gsm_option.3	\
		$(MAN)/gsm_print.3

TOAST_MANUALS =	$(MAN)/toast.1

MANUALS	= 	$(GSM_MANUALS) $(TOAST_MANUALS) $(MAN)/bitter.1

# Other stuff in the distribution

STUFF = 	ChangeLog			\
		INSTALL			\
		MACHINES		\
		MANIFEST		\
		Makefile		\
		README			\
		$(ADDTST)/add_test.dta	\
		$(TLS)/bitter.dta	\
		$(TST)/run


# Install targets

GSM_INSTALL_TARGETS =	\
		$(GSM_INSTALL_LIB)/libgsm.a		\
		$(GSM_INSTALL_INC)/gsm.h		\
		$(GSM_INSTALL_MAN)/gsm.3		\
		$(GSM_INSTALL_MAN)/gsm_explode.3	\
		$(GSM_INSTALL_MAN)/gsm_option.3		\
		$(GSM_INSTALL_MAN)/gsm_print.3

TOAST_INSTALL_TARGETS =	\
		$(TOAST_INSTALL_BIN)/toast		\
		$(TOAST_INSTALL_BIN)/tcat		\
		$(TOAST_INSTALL_BIN)/untoast		\
		$(TOAST_INSTALL_MAN)/toast.1


# Default rules

include $(ASTTOPDIR)/Makefile.rules

# Target rules

all:		$(LIBGSM) $(LIBGSMSO) $(TOAST) $(TCAT) $(UNTOAST)
		@-echo $(ROOT): Done.

tst:		$(TST)/lin2cod $(TST)/cod2lin $(TOAST) $(TST)/test-result
		@-echo tst: Done.

addtst:		$(ADDTST)/add $(ADDTST)/add_test.dta
		$(ADDTST)/add < $(ADDTST)/add_test.dta > /dev/null
		@-echo addtst: Done.

misc:		$(TLS)/sweet $(TLS)/bitter $(TLS)/sour $(TLS)/ginger 	\
			$(TST)/lin2txt $(TST)/cod2txt $(TST)/gsm2cod
		@-echo misc: Done.

install:	toastinstall gsminstall
		@-echo install: Done.


# The basic API: libgsm

$(LIBGSMSO):	$(LIB) $(GSM_OBJECTS)
		$(LD) -o $@.1.0.10 -shared -Xlinker -soname -Xlinker libgsm.so.1 $(GSM_OBJECTS) -lc
		ln -fs libgsm.so.1.0.10 lib/libgsm.so.1
		ln -fs libgsm.so.1.0.10 lib/libgsm.so

$(LIBGSM): $(GSM_OBJECTS)
	$(ECHO_PREFIX) echo "   [AR] $^ -> $@"
	$(CMD_PREFIX) $(AR) cr $@ $^
	$(CMD_PREFIX) $(RANLIB) $@


# Toast, Untoast and Tcat -- the compress-like frontends to gsm.

$(TOAST):	$(BIN) $(TOAST_OBJECTS) $(LIBGSM)
		$(LD) $(LFLAGS) -o $(TOAST) $(TOAST_OBJECTS) $(LIBGSMSO) $(LDLIB)

$(UNTOAST):	$(BIN) $(TOAST)
		-rm $(RMFLAGS) $(UNTOAST)
		$(LN) toast $(UNTOAST)

$(TCAT):	$(BIN) $(TOAST)
		-rm $(RMFLAGS) $(TCAT)
		$(LN) toast $(TCAT)


# The local bin and lib directories

$(BIN):
		if [ ! -d $(BIN) ] ; then mkdir $(BIN) ; fi

$(LIB):
		if [ ! -d $(LIB) ] ; then mkdir $(LIB) ; fi


# Installation

gsminstall:
		-if [ x"$(GSM_INSTALL_ROOT)" != x ] ; then	\
			$(MAKE) $(GSM_INSTALL_TARGETS) ;	\
		fi

toastinstall:
		-if [ x"$(TOAST_INSTALL_ROOT)" != x ]; then	\
			$(MAKE) $(TOAST_INSTALL_TARGETS);	\
		fi

gsmuninstall:
		-if [ x"$(GSM_INSTALL_ROOT)" != x ] ; then	\
			rm $(RMFLAGS) $(GSM_INSTALL_TARGETS) ;	\
		fi

toastuninstall:
		-if [ x"$(TOAST_INSTALL_ROOT)" != x ] ; then 	\
			rm $(RMFLAGS) $(TOAST_INSTALL_TARGETS);	\
		fi

$(TOAST_INSTALL_BIN)/toast:	$(TOAST)
		-rm $@
		cp $(TOAST) $@
		chmod 755 $@

$(TOAST_INSTALL_BIN)/untoast:	$(TOAST_INSTALL_BIN)/toast
		-rm $@
		ln $? $@

$(TOAST_INSTALL_BIN)/tcat:	$(TOAST_INSTALL_BIN)/toast
		-rm $@
		ln $? $@

$(TOAST_INSTALL_MAN)/toast.1:	$(MAN)/toast.1
		-rm $@
		cp $? $@
		chmod 444 $@

$(GSM_INSTALL_MAN)/gsm.3:	$(MAN)/gsm.3
		-rm $@
		cp $? $@
		chmod 444 $@

$(GSM_INSTALL_MAN)/gsm_option.3:	$(MAN)/gsm_option.3
		-rm $@
		cp $? $@
		chmod 444 $@

$(GSM_INSTALL_MAN)/gsm_explode.3:	$(MAN)/gsm_explode.3
		-rm $@
		cp $? $@
		chmod 444 $@

$(GSM_INSTALL_MAN)/gsm_print.3:	$(MAN)/gsm_print.3
		-rm $@
		cp $? $@
		chmod 444 $@

$(GSM_INSTALL_INC)/gsm.h:	$(INC)/gsm.h
		-rm $@
		cp $? $@
		chmod 444 $@

$(GSM_INSTALL_LIB)/libgsm.a:	$(LIBGSM)
		-rm $@
		cp $? $@
		chmod 444 $@


# Distribution

dist:		gsm-1.0.tar.Z
		@echo dist: Done.

gsm-1.0.tar.Z:	$(STUFF) $(SOURCES) $(HEADERS) $(MANUALS)
		(	cd $(ROOT)/..;				\
			tar cvf - `cat $(ROOT)/gsm-1.0/MANIFEST	\
				| sed '/^#/d'`			\
		) | $(COMPRESS) $(COMPRESSFLAGS) > $(ROOT)/gsm-1.0.tar.Z

# Clean

uninstall:	toastuninstall gsmuninstall
		@-echo uninstall: Done.

semi-clean:
		-rm $(RMFLAGS)  */*.o			\
			$(TST)/lin2cod $(TST)/lin2txt	\
			$(TST)/cod2lin $(TST)/cod2txt	\
			$(TST)/gsm2cod 			\
			$(TST)/*.*.*
		-$(FIND) . \( -name core -o -name foo \) \
			-print | xargs rm $(RMFLAGS)

clean:	semi-clean
		-rm $(RMFLAGS) $(LIBGSM) $(ADDTST)/add		\
			$(TOAST) $(TCAT) $(UNTOAST)	\
			$(ROOT)/gsm-1.0.tar.Z
		rm -rf lib
		rm -f .*.d

# Two tools that helped me generate gsm_encode.c and gsm_decode.c,
# but aren't generally needed to port this.

$(TLS)/sweet:	$(TLS)/sweet.o $(TLS)/taste.o
		$(LD) $(LFLAGS) -o $(TLS)/sweet \
			$(TLS)/sweet.o $(TLS)/taste.o $(LDLIB)

$(TLS)/bitter:	$(TLS)/bitter.o $(TLS)/taste.o
		$(LD) $(LFLAGS) -o $(TLS)/bitter \
			$(TLS)/bitter.o $(TLS)/taste.o $(LDLIB)

# A version of the same family that Jeff Chilton used to implement
# the WAV #49 GSM format.

$(TLS)/ginger:	$(TLS)/ginger.o $(TLS)/taste.o
		$(LD) $(LFLAGS) -o $(TLS)/ginger \
			$(TLS)/ginger.o $(TLS)/taste.o $(LDLIB)

$(TLS)/sour:	$(TLS)/sour.o $(TLS)/taste.o
		$(LD) $(LFLAGS) -o $(TLS)/sour \
			$(TLS)/sour.o $(TLS)/taste.o $(LDLIB)

# Run $(ADDTST)/add < $(ADDTST)/add_test.dta to make sure the
# basic arithmetic functions work as intended.

$(ADDTST)/add:	$(ADDTST)/add_test.o
		$(LD) $(LFLAGS) -o $(ADDTST)/add $(ADDTST)/add_test.o $(LDLIB)


# Various conversion programs between linear, text, .gsm and the code
# format used by the tests we ran (.cod).  We paid for the test data,
# so I guess we can't just provide them with this package.  Still,
# if you happen to have them lying around, here's the code.
# 
# You can use gsm2cod | cod2txt independently to look at what's
# coded inside the compressed frames, although this shouldn't be
# hard to roll on your own using the gsm_print() function from
# the API.


$(TST)/test-result:	$(TST)/lin2cod $(TST)/cod2lin $(TOAST) $(TST)/run
			( cd $(TST); ./run ) 

$(TST)/lin2txt:		$(TST)/lin2txt.o $(LIBGSM)
			$(LD) $(LFLAGS) -o $(TST)/lin2txt \
				$(TST)/lin2txt.o $(LIBGSM) $(LDLIB)

$(TST)/lin2cod:		$(TST)/lin2cod.o $(LIBGSM)
			$(LD) $(LFLAGS) -o $(TST)/lin2cod \
				$(TST)/lin2cod.o $(LIBGSM) $(LDLIB)

$(TST)/gsm2cod:		$(TST)/gsm2cod.o $(LIBGSM)
			$(LD) $(LFLAGS) -o $(TST)/gsm2cod \
				$(TST)/gsm2cod.o $(LIBGSM) $(LDLIB)

$(TST)/cod2txt:		$(TST)/cod2txt.o $(LIBGSM)
			$(LD) $(LFLAGS) -o $(TST)/cod2txt \
				$(TST)/cod2txt.o $(LIBGSM) $(LDLIB)

$(TST)/cod2lin:		$(TST)/cod2lin.o $(LIBGSM)
			$(LD) $(LFLAGS) -o $(TST)/cod2lin \
				$(TST)/cod2lin.o $(LIBGSM) $(LDLIB)
