#
# Makefile example for WiiMote code in libkondo4
#
# Copyright 2010 - Christopher Vo (cvo1@cs.gmu.edu)
# George Mason University - Autonomous Robotics Laboratory
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

CC:=gcc
LD:=$(CC)
LIBKONDO_LDFLAGS:=-L../ -lkondo
LIBKONDO_INCLUDE:=-I../
LIBWIIUSE_LDFLAGS:=-lwiiuse

CFLAGS:=-fPIC -O2 ${LIBKONDO_INCLUDE}
LDFLAGS:=-lm -Wl,-rpath,. -Wl,-rpath,../ -fPIC \
	${LIBKONDO_LDFLAGS} \
	${LIBWIIUSE_LDFLAGS}
SRCS:=$(wildcard *.c)
OBJS:=$(SRCS:.c=.o)
DEPS:=$(SRCS:.c=.d)
PROGS:=$(basename ${SRCS})

all: $(PROGS)

clean:
	rm -rf Dependencies *~
	rm -rf $(PROGS) $(OBJS) $(DEPS)
	
$(PROGS) : % : %.o
	$(LD) $(LDFLAGS) -o $@ $@.o

%.o : %.c
	$(CC) $(CFLAGS) -MMD -c $< -o $@
	@cat $*.d >> Dependencies
	@rm -f $*.d
	
-include Dependencies
