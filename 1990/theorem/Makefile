#!/usr/bin/env make
#
# IOCCC 1990 winning entry - theorem

################################################################################
#
# IOCCC winning entry code may not work on your system.  What was liked/allowed
# and worked in the past may no longer be liked/allowed or compile/run today.
#
# Bug fixes, corrections and typo fixes are VERY WELCOME.  If you see a problem,
# first check this URL for a list of known bugs and (mis)features of IOCCC entries:
#
#	https://www.ioccc.org/bugs.html
#
# GitHub pull requests are welcome!  Please see the above URL for details.
#
################################################################################
#
# This file is Copyright (c) 2023 by Landon Curt Noll.  All Rights Reserved.
# You are free to share and adapt this file under the terms of this license:
#
#	Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)
#
# For more information, see: https://creativecommons.org/licenses/by-sa/4.0/


#############################
# shell used by this Makefile
#############################
#
SHELL= bash

#######################
# common tool locations
#######################
#
include ../../var.mk

# Common C compiler warnings to silence
#
CSILENCE= -Wno-deprecated-declarations -Wno-empty-body -Wno-error -Wno-unused-value \
	  -Wno-implicit-function-declaration -Wno-incompatible-pointer-types \
	  -Wno-macro-redefined -Wno-parentheses -Wno-return-type \
	  -Wno-unused-parameter -Wno-empty-translation-unit \
	  -Wno-deprecated-non-prototype -Wno-int-conversion -Wno-strict-prototypes \
	  -Wno-implicit-int

# Attempt to silence unknown warning option
#
CUNKNOWN= -Wno-unknown-warning-option

# Common C compiler warning flags
#
CWARN= -Wall -Wextra ${CSILENCE} ${CUNKNOWN}

# Compiler standard
#
CSTD= -std=gnu90

# Compiler bit architecture
#
ARCH=

# Defines that are needed to compile
#
CDEFINE=

# Include files that are needed to compile
#
CINCLUDE=

# Optimization
#
OPT= -O3

# Default flags for ANSI C compilation
#
CFLAGS= ${CSTD} ${CWARN} ${ARCH} ${CDEFINE} ${CINCLUDE} ${OPT}

# Libraries needed to build
#
LDFLAGS=

# C compiler to use
#
CC= cc

# Compiler add-ons or replacements for clang only
#
ifeq "$(findstring $(CLANG),${CC})" "$(CLANG)"
#
CSILENCE+= -Wno-comma -Wno-double-promotion -Wno-float-conversion \
	   -Wno-missing-prototypes -Wno-missing-variable-declarations \
	   -Wno-poison-system-directories -Wno-shadow -Wno-strict-prototypes \
	   -Wno-unreachable-code -Wno-unused-macros -Wno-implicit-float-conversion \
	   -Wno-extra-semi-stmt -Wno-unsafe-buffer-usage
#
CWARN+= -Weverything
#
endif

# Specific add-ons or replacements for gcc only
#
ifeq "$(findstring $(GCC),${CC})" "$(GCC)"
#
#CSILENCE+=
#
#CWARN+=
#
endif


##############################
# Special Makefile variables for this entry
##############################
#
ENTRY= theorem
PROG= ${ENTRY}
#
OBJ= ${PROG}.o
DATA=
TARGET= ${PROG} sorter fibonacci theorem_bkp
#
ALT_OBJ=
ALT_TARGET=


#################
# build the entry
#################
#
all: data ${TARGET}
	@${TRUE}

.PHONY: all alt data everything clean clobber

${PROG}: ${PROG}.c
	${CC} ${CFLAGS} $< -o $@ ${LDFLAGS}

sorter.c: ${PROG} ${PROG}.c
	-./theorem -r 0 0 0 0 < theorem.c > sorter.c

sorter: sorter.c
	${CC} ${CFLAGS} sorter.c -o $@

fibonacci.c: sorter ${PROG}.c
	-./sorter 0 0 0 0 < theorem.c > fibonacci.c

fibonacci: fibonacci.c
	${CC} ${CFLAGS} fibonacci.c -o $@

theorem_bkp: sorter theorem_bkp.c
	${CC} ${CFLAGS} theorem_bkp.c -o $@

theorem_bkp.c:
	${RM} -f $@
	-./sorter -r 0 0 0 0 < sorter.c > theorem_bkp.c

# alternative executable
#
alt: data ${ALT_TARGET}
	@${TRUE}

# data files
#
data: ${DATA}
	@${TRUE}

# both all and alt
#
everything: all alt
	@${TRUE}


###############
# utility rules
###############
#
clean:
	${RM} -f ${OBJ} ${ALT_OBJ}

clobber: clean
	${RM} -f ${TARGET} ${ALT_TARGET}
	${RM} -rf *.dSYM
	${RM} -f sorter.c sorter
	${RM} -f fibonacci.c fibonacci
	${RM} -f theorem_bkp.c theorem_bkp


######################################
# optional include of 1337 hacker rulz
######################################

-include 1337.mk ../1337.mk ../../1337.mk
