#

SHELL = /bin/sh

TOP     = $(PWD)

CROSS   =
CC      = $(CROSS)gcc
LD      = $(CROSS)ld
YACC	= bison
YFLAGS	= -d -y
LEX	= flex
LFLAGS	=
OBJCOPY = $(CROSS)objcopy

CFLAGS  += -g -O2 -Wall -DAIO -DFALLOCATE -D_GNU_SOURCE
LDFLAGS =
LIBS    = -laio

export SHELL TOP CC LD CFLAGS LDFLAGS

TARGET  = fsx-linux

OBJS    = fsx-linux.o
GENERATE_SOURCE =

all: $(TARGET)

FORCE:
#	$(MAKE) -C lib

$(TARGET): FORCE $(OBJS)
	$(CC) $(CFLAGS) $(LDFLAGS) -o $(TARGET) $(OBJS) $(LIBS)

.S.o:
	$(CC) -Wp,-MD,$(@D)/.$(@F).d -D_ASSEMBLER_ $(CFLAGS) -c -o $@ $<

.c.o:
	$(CC) -Wp,-MD,$(@D)/.$(@F).d $(CFLAGS) -c -o $@ $<

clean:
	-rm -f $(OBJS) $(depend_files) $(TARGET) $(GENERATE_SOURCE) core core.*

# include dependency files (.foo.o.d ../bar/.baz.o.d ...)
depend_files = $(join $(dir $(OBJS)),$(patsubst %.o,.%.o.d,$(notdir $(OBJS))))
-include $(depend_files)
