CC=gcc
SONAME=-soname
FRAMEWORK=
LDFLAGS=-lftdi 
CFLAGS=-Wall -fPIC -fno-strict-aliasing -g -O2
LIBFTDI1=0
prefix=/usr/local
exec_prefix=${prefix}
LIBDIR=${exec_prefix}/lib
INCDIR=${prefix}/include
TARGET=mpsse

.PHONY: examples install uninstall clean distclean

all: $(TARGET)

$(TARGET): mpsse.o fast.o
	$(CC) $(CFLAGS) -shared -Wl,$(SONAME),lib$(TARGET).so *.o -o lib$(TARGET).so $(LDFLAGS)
	ar rcs lib$(TARGET).a *.o

examples:
	make -C examples

mpsse.o: support.o
	$(CC) $(CFLAGS) $(LDFLAGS) -DLIBFTDI1=$(LIBFTDI1) -c mpsse.c

fast.o: support.o
	$(CC) $(CFLAGS) $(LDFLAGS) -DLIBFTDI1=$(LIBFTDI1) -c fast.c

support.o:
	$(CC) $(CFLAGS) $(LDFLAGS) -DLIBFTDI1=$(LIBFTDI1) -c support.c

install:
	install -D -m644 lib$(TARGET).so $(DESTDIR)/$(LIBDIR)/lib$(TARGET).so
	install -D -m644 lib$(TARGET).a  $(DESTDIR)/$(LIBDIR)/lib$(TARGET).a
	install -D -m644 $(TARGET).h     $(DESTDIR)/$(INCDIR)/$(TARGET).h

uninstall: py$(BUILD)-uninstall
	rm -f $(DESTDIR)/$(LIBDIR)/lib$(TARGET).so \
		$(DESTDIR)/$(LIBDIR)/lib$(TARGET).a \
		$(DESTDIR)/$(INCDIR)/$(TARGET).h

clean:
	make -C examples clean
	rm -rf *.o *.so *.a

distclean: clean
	rm -rf *.cache config.* Makefile

