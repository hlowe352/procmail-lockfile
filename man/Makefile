
LOCKINGTEST=__defaults__

#LOCKINGTEST=/tmp .	# Uncomment and add any directories you see fit.
#			If LOCKINGTEST is defined, autoconf will NOT
#			prompt you to enter additional directories.
#			See INSTALL for more information about the
#			significance of the locking tests.

########################################################################
# Only edit below this line if you *think* you know what you are doing #
########################################################################

#LOCKINGTEST=100	# Uncomment (and change) if you think you know
#			it better than the autoconf lockingtests.
#			This will cause the lockingtests to be hotwired.
#			100	to enable fcntl()
#			010	to enable lockf()
#			001	to enable flock()
#			Or them together to get the desired combination.

# Optional system libraries we search for
SEARCHLIBS = -lm -ldir -lx -lsocket -lnet -linet -lnsl_s -lnsl_i -lnsl -lsun \
 -lgen -lsockdns -ldl
#			-lresolv	# not really needed, is it?

# Informal list of directories where we look for the libraries in SEARCHLIBS
LIBPATHS=/lib /usr/lib /usr/local/lib

GCC_WARNINGS = -O2 -pedantic -Wreturn-type -Wunused -Wformat -Wtraditional \
 -Wpointer-arith -Wconversion -Waggregate-return \
 #-Wimplicit -Wshadow -Wid-clash-6 #-Wuninitialized

# The place to put your favourite extra cc flag
CFLAGS0 = -O -Wno-implicit-function-declaration -Wno-comment -Wno-deprecated-non-prototype #$(GCC_WARNINGS)
LDFLAGS0= -s
# Read my libs :-)
LIBS=

CFLAGS1 = $(CFLAGS0) #-posix -Xp
LDFLAGS1= $(LDFLAGS0) $(LIBS) #-lcposix

####CC	= cc # gcc
# object file extension
O	= o
RM	= /bin/rm -f
MV	= mv -f
LN	= ln
BSHELL	= /bin/sh
INSTALL = cp
DEVNULL = /dev/null
STRIP	= strip
MKDIRS	= new/mkinstalldirs

SUBDIRS = src man
BINSS	= lockfile
MANS1S	= lockfile
MANS5S	=

# Possible locations for the sendmail.cf file
SENDMAILCFS = /etc/mail/sendmail.cf /etc/sendmail.cf /usr/lib/sendmail.cf

# Makefile.1 - mark, don't (re)move this, a sed script needs it

FGREP	= grep -F
STRIP	= 
CFLAGS	= $(CFLAGS1) -std=gnu89  
LDFLAGS	= $(LDFLAGS1) -lm -ldl -lc

BINS= new/lockfile
MANS= new/lockfile.1
MANS1= lockfile.$(MAN1SUFFIX)
MANS5=
MANSS= lockfile.1
NBINS= ../new/lockfile
NMANS= ../new/lockfile.1


#$Id$

all: $(MANSS)

make:
	@$(SHELL) -c "exit 0"

.PRECIOUS: Makefile

../config.check:
	@cd ..; $(MAKE) config.check

man.sed: man_sed

man_sed:
	@cd ../src; $(MAKE) ../man/man.sed

clean:
	$(RM) $(MANSS) man.sed* _Makefile *core*

Makefile: ../Makefile Makefile.0
	@echo "You have made changes to the master Makefile, in order for"
	@echo "these changes to show through, you will first have to do:"
	@echo "$(MAKE) makefiles"

makefiles Makefiles makefile:
	cd ..; $(MAKE) makefiles

init:
	cd ..; $(MAKE) $@

../new/lockfile.1: lockfile.1 ../config.check
	@test -d ../new || mkdir ../new
	@$(RM) $@
	$(LN) ../man/lockfile.1 $@

lockfile.1: lockfile.man man.sed mansed
	$(SHELL) ./mansed $(SHELL) lockfile.man $@ "$(RM)" $(DEVNULL)
#
