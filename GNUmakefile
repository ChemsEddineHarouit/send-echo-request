prefix     = /usr
execprefix = $(prefix)
bindir     = $(execprefix)/bin

INSTALL = install

crossprefix =

crossCC      = $(crossprefix)gcc
crossNM      = $(crossprefix)nm
crossOBJDUMP = $(crossprefix)objdump
crossSTRIP   = $(crossprefix)strip

CC      = gcc
NM      = nm
OBJDUMP = objdump
STRIP   = strip

CLEANFILES =

DUMMY1 := $(shell ./update-git-version.sh)
CLEANFILES += git-version.h

DUMMY2 := $(shell ./update-usage-msg.sh)
CLEANFILES += usage-msg.h

BASE = send-echo-request
export BASE

.PHONY: all
all:
	mkdir -p host
	$(MAKE) -f rules.mk outdir=host  CC=$(CC)      NM=$(NM)      OBJDUMP=$(OBJDUMP)      STRIP=$(STRIP)
ifneq ($(crossprefix),)
	mkdir -p cross
	$(MAKE) -f rules.mk outdir=cross CC=$(crossCC) NM=$(crossNM) OBJDUMP=$(crossOBJDUMP) STRIP=$(crossSTRIP)
endif

.PHONY: clean
clean:
	rm -f $(CLEANFILES)
	rm -rf cross host

.PHONY: install
install: all
	$(INSTALL) -c  -m 0755 -d               $(DESTDIR)$(bindir)
	$(INSTALL) -cp -m 0755 host/$(BASE).exe $(DESTDIR)$(bindir)/$(BASE)

.PHONY: uninstall
uninstall:
	rm -f $(DESTDIR)$(bindir)/$(BASE)
