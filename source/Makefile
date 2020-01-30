MKLLIB=/anaconda3/lib/
FCC=gfortran

FFLAGS= -fPIC -O3 -Wall
FINCLUDE= -I../include/
DATE  = $(shell date)

fmain=program_dftd.o
ftests = tests_dftd.o assertion.o class_molecule.o geometry_reader.o eeq_model.o dftd4.o pbc_tools.o
fsrcs = class_wsc.o pbc_tools.o class_molecule.o class_param.o printout.o mctc_environment.o error.o class_set.o class_results.o coordination_number.o eeq_model.o  dftd4.o argparser.o dfuncpar.o geometry_reader.o disp_output.o d4_calculation.o c_api.o f_api.o pbc.o
mctc= mctc_global.o mctc_systools.o mctc_readin.o mctc_strings.o mctc_constants.o mctc_econv.o mctc_param.o mctc_timings.o 

OBJ = $(mctc) $(fsrcs) $(fmain)

all: main

OBJ = $(mctc) $(fsrcs) $(fmain)

ifeq ($(MKLLIB), 0) 
main:
	@echo "Please provide MKLLIB!!!"
else
main: version $(OBJ)
	$(FCC) -o d4.exe $(OBJ) $(LIB) -Wl,-rpath,"$(MKLLIB)" 
endif

MKL=$(shell python -c 'import os; print(" ".join(os.path.join("$(MKLLIB)", file) for file in os.listdir("$(MKLLIB)") if any("lib%s" % pattern in file for pattern in ("mkl_intel_lp64", "mkl_core", "mkl_sequential"))))')

LIB= -lpthread -lm $(MKL)

tests: $(ftests)
	$(FCC) -o tests.exe $(ftests) $(LIB)

lib: version $(mctc) $(fsrcs) 
	$(FCC) -o libdftd4.so -shared $(fsrcs) $(LIB)

clear:
	rm *.o *.mod *.so

version: 
	@echo 'character(len=*),parameter :: version = "2.3.2"' > dftd4_version.fh
	@echo 'character(len=*),parameter :: date = "$(DATE)"' >> dftd4_version.fh
	@echo 'character(len=*),parameter :: author = "$(USER)@$(HOST)"' >> dftd4_version.fh

%.o: %.f90
	$(FCC) $(FINCLUDE) $(FFLAGS) -c $<


