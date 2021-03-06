# In this Makefile, we add a rule for generating .o files from .c source files

# We also use the $@ and $^ variables in the rule for hello.exe
# to refer to hello.exe and {hello.c hellofunc.c} respectively.

# Finally, we include the file machine.def, which defines
# our compiler and compiler-flag variables.  These may change
# from machine to machine.

# As a result, only machine.def needs to be changed
# when moving our work to a new machine

include machine.def

CFLAGS        = $(OPT_FLAGS) $(INCLUDE_FLAGS) -I pkg1/include
LIBSHARED     = 
LIBSTATIC     = 
PROG_STATIC   = test.static
PROG_DYNAMIC  = test.dynamic
PROG_RPATH    = test.rpath
PROG_ORIGIN   = test.origin
PROGS = $(PROG_DYNAMIC) $(PROG_STATIC) $(PROG_RPATH) $(PROG_ORIGIN)

.PHONY: clean libs all

all: $(PROGS) main.c

$(PROG_STATIC): main.c libs
	$(CC) $(CFLAGS) main.c $(LIBSTATIC) -o $@

$(PROG_DYNAMIC): main.c libs
	$(CC) $(CFLAGS) main.c $(LIBSHARED) -o $@

$(PROG_RPATH): main.c libs
	$(CC) $(CFLAGS) main.c $(LIBSHARED)  -Wl,-rpath,$(PWD)/pkg1/lib -o $@

$(PROG_ORIGIN): main.c libs
	$(CC) $(CFLAGS) main.c $(LIBSHARED)  -Wl,-rpath,"\$$ORIGIN"/lib -o $@

libs:
	@$(MAKE) --no-print-directory -C pkg1/src all
	@$(MAKE) --no-print-directory -C pkg2/src all

clean:
	rm -f *.o
	rm -f $(PROG_STATIC) 
	rm -f $(PROG_DYNAMIC) 
	rm -f $(PROG_RPATH) 
