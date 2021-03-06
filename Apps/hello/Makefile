#******************************************************************************
#
# Makefile
#
#*****************************************************************************

#
# ROOT_PATH comes from global shell environment.
# Ensure run `source envsetup.sh` first of all.
#
#ifndef ROOT_PATH
#	ROOT_PATH := ../..
#endif

#
# Include the common make definitions.
#
include ${ROOT_PATH}/makedefs

#
# Path and directory
#
MKFILE_PATH  := $(abspath $(lastword $(MAKEFILE_LIST)))
CURRENT_PATH := $(shell pwd)
CURRENT_DIR  := $(notdir $(CURDIR:%/=%))

#
# The base directory for SDK
#
SDK_ROOT=../../SDK/CC3200

#
# Target
#
TARGET_NAME := ${CURRENT_DIR}

#
# Where to find source files that do not live in this directory.
#
VPATH  = .
VPATH += ../common

#
# Where to find header files that do not live in the source directory.
#
IPATH  = .
IPATH += ../inc
IPATH += ../common
IPATH += ${SDK_ROOT}/inc
IPATH += ${SDK_ROOT}/driverlib

#
# The default rule, which causes the driver library to be built.
#
all: ${OBJDIR} ${BINDIR}
all: ${BINDIR}/${TARGET_NAME}.axf

#
# The rule to clean out all the build products.
#
clean:
	rm -rf ${OBJDIR} ${wildcard *~}
	rm -rf ${BINDIR} ${wildcard *~}


#
# The rule to create the target directories.
#
${OBJDIR}:
	@mkdir -p ${OBJDIR}

${BINDIR}:
	@mkdir -p ${BINDIR}

#
# Rules for building the target
#
${BINDIR}/${TARGET_NAME}.axf: ${OBJDIR}/main.o
${BINDIR}/${TARGET_NAME}.axf: ${OBJDIR}/pinmux.o
${BINDIR}/${TARGET_NAME}.axf: ${OBJDIR}/gpio_if.o
${BINDIR}/${TARGET_NAME}.axf: ${OBJDIR}/startup_${COMPILER}.o
${BINDIR}/${TARGET_NAME}.axf: ${SDK_ROOT}/driverlib/${COMPILER}/${BINDIR}/libdriver.a

SCATTERgcc_${TARGET_NAME} = linker.ld
ENTRY_${TARGET_NAME} = ResetISR

#
# Include the automatically generated dependency files.
#
ifneq (${MAKECMDGOALS}, clean)
-include ${wildcard ${OBJDIR}/*.d} __dummy__
endif
