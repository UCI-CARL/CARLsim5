##----------------------------------------------------------------------------##
##
##   CARLsim4 CARLsim-ECJ PTI interface examples Makefile
##   -------------------------
##
##   Authors:   Eric Scott <escott8@gmu.edu>
##				Michael Beyeler <mbeyeler@uci.edu>
##              Kristofor Carlson <kdcarlso@uci.edu>
##
##   Institute: Cognitive Anteater Robotics Lab (CARL)
##              Department of Cognitive Sciences
##              University of California, Irvine
##              Irvine, CA, 92697-5100, USA
##
##   Version:   04/11/2018, HK
##
##----------------------------------------------------------------------------##

#------------------------------------------------------------------------------
# Include configuration file
#------------------------------------------------------------------------------

# NOTE: If your CARLsim4 installation does not reside in the default path, make
# sure the environment variable CARLSIM4_INSTALL_DIR is set.
ifdef CARLSIM5_INSTALL_DIR
	CARLSIM5_INC_DIR  := $(CARLSIM5_INSTALL_DIR)/include
else
	CARLSIM5_INC_DIR  := $(HOME)/CARL/include
endif

# include compile flags etc.
include $(CARLSIM5_INC_DIR)/configure.mk

#------------------------------------------------------------------------------
# Build local variables
#------------------------------------------------------------------------------

cpp_files  := $(wildcard *.cpp)
targets := $(patsubst %.cpp, %, $(cpp_files))
obj_files    := $(patsubst %.cpp, obj/%.o, $(cpp_files))

# handled by clean
clean_files := $(obj_files) $(patsubst %, %.out, $(targets))

#------------------------------------------------------------------------------
# Project targets and rules
#------------------------------------------------------------------------------

.PHONY: clean distclean help all
default: all

all: $(targets)

$(targets): %: obj/%.o
	$(CXX) $(CARLSIM5_FLG) $< -o $@.out $(CARLSIM5_LIB) $(pti_lib)

obj/%.o: %.cpp
	@test -d obj/ || mkdir -p obj/
	$(CXX) -c $(CARLSIM5_FLG) $(CXXINCFL) $(CXXFL) $< -o $@

clean:
	$(RM) $(clean_files)

help:
	$(info CARLsim PTI examples Makefile options:)
	$(info )
	$(info make all	       Compiles all examples)
	$(info make clean	   Cleans out all compiled files)
	$(info make help	   Brings up this message)
