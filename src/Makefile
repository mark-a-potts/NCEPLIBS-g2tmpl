SHELL=/bin/sh
# sources, headers, objects, library and etc.
SRCS_C  = process_4dot2.c
SRCS_F  = grib2_all_tables_module.f \
          g2sec4_temp11.f g2sec4_temp1.f  \
          g2sec4_temp12.f gdtsec3.f
OBJS    = $(patsubst %.c, %.o, $(SRCS_C)) \
          $(patsubst %.f, %.o, $(SRCS_F))

all: build

build: $(LIB)

$(LIB): $(OBJS)
	$(AR) $(ARFLAGS) $@ $^

debug: dbg_build

dbg_build: override CFLAGS += $(DEBUG)
dbg_build: override FFLAGS += $(DEBUG)
dbg_build: $(LIB)

%.o: %.c
	$(CC) -c $(CFLAGS) $(CFLAGSDEFS) $<

%.o: %.f
	$(FC) -c $(FREEFORM) $(FFLAGS) $(FFLAGSDEFS) $<

message: $(MSGSRC)
	$(CC) -c $(MSGSRC)
	$(AR) $(ARFLAGS) $(LIB) $(patsubst %.c, %.o, $(MSGSRC))
	$(RM) $(MSGSRC) $(patsubst %.c, %.o, $(MSGSRC))

install:
	[[ -z "$(LIB)" || -z "$(LIB_DIR)" ]] || mv $(LIB) $(LIB_DIR)
	[[ -z "$(MOD)" || -z "$(INC_DIR)" ]] || mv $(MOD) $(INC_DIR)
	[[ -z "$(SRC_DIR)" ]] || cp ./* $(SRC_DIR)

test:
	@echo "*** unit test unavailable currently ***"

clean:
	$(RM) $(OBJS) $(LIB)
	[[ -z "$(MOD)" ]] || $(RM) -r $(MOD)

.SUFFIXES: .f .mod .c .o .a

# Specify targets that do not generate filesystem objects
.PHONY: all build install debug dbg_build message test clean
