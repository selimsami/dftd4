MKLLIB=  # Please set this!
FCC=gfortran

FFLAGS= -fPIC -O3 -Wall
FINCLUDE= -I../include/

fmain=program_dftd.o
ftests = tests_dftd.o assertion.o class_molecule.o geometry_reader.o eeq_model.o dftd4.o pbc_tools.o
fsrcs = class_wsc.o pbc_tools.o class_molecule.o class_param.o printout.o mctc_environment.o error.o class_set.o class_results.o coordination_number.o eeq_model.o  dftd4.o argparser.o dfuncpar.o geometry_reader.o disp_output.o d4_calculation.o c_api.o f_api.o pbc.o
mctc= mctc_global.o mctc_systools.o mctc_readin.o mctc_strings.o mctc_constants.o mctc_econv.o mctc_param.o mctc_timings.o 

LIB= -L$(MKLLIB) -lmkl_intel_lp64 -lmkl_core -lmkl_sequential -lpthread -lm


OBJ = $(mctc) $(fsrcs) $(fmain)

all: main

main: version $(OBJ)
	$(FCC) -o d4.exe $(OBJ) $(LIB) 

tests: $(ftests)
	$(FCC) -o tests.exe $(ftests) $(LIB)

lib: version $(mctc) $(fsrcs) 
	$(FCC) -o libdftd4.so -shared $(fsrcs) $(LIB)

clear:
	rm *.o *.mod *.so

DATE  = $(shell date)

version: 
	@echo 'character(len=*),parameter :: version = "2.3.2"' > dftd4_version.fh
	@echo 'character(len=*),parameter :: date = "$(DATE)"' >> dftd4_version.fh
	@echo 'character(len=*),parameter :: author = "$(USER)@$(HOST)"' >> dftd4_version.fh

%.o: %.f90
	$(FCC) $(FINCLUDE) $(FFLAGS) -c $<


