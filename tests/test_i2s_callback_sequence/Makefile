ifeq ($(USING_XWAF),1)
all:
	xwaf configure build --config $(CONFIG)
else # USING_XWAF
# The TARGET variable determines what target system the application is
# compiled for. It either refers to an XN file in the source directories
# or a valid argument for the --target option when compiling
TARGET = SLICEKIT-A16

# The APP_NAME variable determines the name of the final .xe file. It should
# not include the .xe postfix. If left blank the name will default to
# the project name
APP_NAME =

# The USED_MODULES variable lists other module used by the application.
USED_MODULES = lib_i2s

# The flags passed to xcc when building the application
# You can also set the following to override flags for a particular language:
# XCC_XC_FLAGS, XCC_C_FLAGS, XCC_ASM_FLAGS, XCC_CPP_FLAGS
# If the variable XCC_MAP_FLAGS is set it overrides the flags passed to
# xcc for the final link (mapping) stage.

$(foreach out,0 1 2 3 4,\
 $(foreach in,0 1 2 3 4,\
   $(eval \
	XCC_FLAGS_master_$(out)$(in) = -O2 -g -DMASTER  -DNUM_OUT=$(out) -DNUM_IN=$(in)\
    )\
   $(eval \
	XCC_FLAGS_slave_$(out)$(in) = -O2 -g -DSLAVE  -DNUM_OUT=$(out) -DNUM_IN=$(in)\
    ) \
 ) \
)

XCC_FLAGS_tdm_118 = -O2 -g -DTDM  -DTDM_CHANS_PER_FRAME=8 -DNUM_OUT=1 -DNUM_IN=1
XCC_FLAGS_tdm_108 = -O2 -g -DTDM  -DTDM_CHANS_PER_FRAME=8 -DNUM_OUT=1 -DNUM_IN=0
XCC_FLAGS_tdm_018 = -O2 -g -DTDM  -DTDM_CHANS_PER_FRAME=8 -DNUM_OUT=0 -DNUM_IN=1
XCC_FLAGS_tdm_224 = -O2 -g -DTDM  -DTDM_CHANS_PER_FRAME=4 -DNUM_OUT=2 -DNUM_IN=2


XCC_FLAGS_i2s_tdm_i2s = -O2 -g -DI2S_TDM_I2S -DI2S_TDM -DNUM_OUT=4 -DNUM_IN=4 -DTDM_CHANS_PER_FRAME=8

XCC_FLAGS_i2s_tdm_tdm = -O2 -g -DI2S_TDM_TDM -DI2S_TDM -DNUM_OUT=4 -DNUM_IN=4 -DTDM_CHANS_PER_FRAME=8

# The XCORE_ARM_PROJECT variable, if set to 1, configures this
# project to create both xCORE and ARM binaries.
XCORE_ARM_PROJECT = 0

# The VERBOSE variable, if set to 1, enables verbose output from the make system.
VERBOSE = 0

XMOS_MAKE_PATH ?= ../..
-include $(XMOS_MAKE_PATH)/xcommon/module_xcommon/build/Makefile.common
endif # USING_XWAF
