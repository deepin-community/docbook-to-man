#
# Copyright 1993 Open Software Foundation, Inc., Cambridge, Massachusetts.
# All rights reserved.
#
# Copyright (c) 1994  
# Open Software Foundation, Inc. 
#  
# Permission is hereby granted to use, copy, modify and freely distribute 
# the software in this file and its documentation for any purpose without 
# fee, provided that the above copyright notice appears in all copies and 
# that both the copyright notice and this permission notice appear in 
# supporting documentation.  Further, provided that the name of Open 
# Software Foundation, Inc. ("OSF") not be used in advertising or 
# publicity pertaining to distribution of the software without prior 
# written permission from OSF.  OSF makes no representations about the 
# suitability of this software for any purpose.  It is provided "as is" 
# without express or implied warranty. 
#
# Copyright (c) 1996 X Consortium
# Copyright (c) 1996 Dalrymple Consulting
# 
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
# 
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
# X CONSORTIUM OR DALRYMPLE CONSULTING BE LIABLE FOR ANY CLAIM, DAMAGES OR
# OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
# ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
# OTHER DEALINGS IN THE SOFTWARE.
# 
# Except as contained in this notice, the names of the X Consortium and
# Dalrymple Consulting shall not be used in advertising or otherwise to
# promote the sale, use or other dealings in this Software without prior
# written authorization.
#
#
# For building 'instant'.
#
# J.Bowe, 1993
#
#  $Header: /aolnet/dev/src/CVS/sgml/docbook-to-man/Instant/Makefile,v 1.3 1999/02/23 22:21:26 db3l Exp $
#
# This assumes you have the (tpt)regexp package (includes and library)
# available.
#
# Some things you could set at your site.
#   XDEFINES   = ...				# for extra defines
#   REGEX_INC  = -I../tptregexp			# should be here with release
#   REGEX_LIB  = ../lib/tptregexp		# assumes you built it there
#   BINDIR     = /usr/local/bin			# where you keep your programs
# (You should set DEF_TPT_LIB to something, or set it in general.h.
# At OSF we use the default in that file.)
#
#   -DSTRERROR to DEFINES if library does not have strerror()   [ANS-db3l]
#
MAKE =	make
SHELL =	/bin/sh

ROOT		= /usr/local

TPTLIB		= $(ROOT)/share/sgml/transpec
REGEX_INC	= -Itptregexp
REGEX_LIB	= tptregexp
BINDIR		= $(ROOT)/bin
DEFINES		= -DDEF_TPT_LIB=\"$(TPTLIB)\" $(XDEFINES)

CC	= gcc

OPT	= -g
CFLAGS	= $(OPT) $(REGEX_INC) $(DEFINES)
LDFLAGS	= $(OPT)
REGEX	= -L$(REGEX_LIB) -ltptregexp

CFILES	= main.c util.c info.c translate.c traninit.c tranvar.c tables.c \
	browse.c
HFILES	= general.h translate.h
OBJ	= main.o util.o info.o translate.o traninit.o tranvar.o tables.o \
	browse.o masterVersion.o
PROGS	= instant

all:	dotptregexp $(PROGS)

dotptregexp:
	cd tptregexp; $(MAKE) all

instant: $(OBJ)
	$(CC) -o $@ $(LDFLAGS) $(OBJ) $(REGEX)

install: all
	cp $(PROGS) $(BINDIR)


Version:	allVersion.o

allVersion.c:	$(HFILES) $(CFILES) Makefile
	co -l allVersion.c
	makeVersionFile $(HFILES) $(CFILES) Makefile > allVersion.c
	ci -u -m"new master version number" allVersion.c
	makeVersionFile -n instant allVersion.c > masterVersion.c


clean:
	rm -f $(OBJ) allVersion.o lint.out core tags
	cd tptregexp; make clean

clobber:	clean
	rm -f $(PROGS)
	cd tptregexp; make clobber

tags: $(CFILES) $(HFILES)
	ctags $(CFILES) $(HFILES)

lint:
	gcc -Wall -Dlint $(REGEX_INC) -c $(CFILES) >lint.out 2>&1
#	lint $(CFILES) > lint.out

# dependencies
main.o:		main.c general.h
util.o:		util.c general.h
info.o:		info.c general.h
translate.o:	translate.c general.h translate.h
traninit.o:	traninit.c general.h translate.h
tranvar.o:	tranvar.c general.h translate.h
tables.o:	tables.c general.h translate.h
browse.o:	browse.c general.h

