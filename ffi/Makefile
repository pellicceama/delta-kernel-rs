BINARY=cffi-test
SOURCES=cffi-test.c
INCPATHS=../target/ffi-headers
LIBPATHS=../target/release
LDFLAGS=-ldelta_kernel_ffi #`pkg-config --libs arrow-glib`
CFLAGS=-c -Wall -DDEFINE_DEFAULT_ENGINE -DDEFINE_SYNC_ENGINE #`pkg-config --cflags arrow-glib`
CC=gcc

OBJECTS=$(SOURCES:.c=.o)
INCFLAGS=$(foreach TMP,$(INCPATHS),-I$(TMP))
LIBFLAGS=$(foreach TMP,$(LIBPATHS),-L$(TMP))

ROOT_DIR:=$(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))

all: $(SOURCES) $(BINARY)

$(BINARY): $(OBJECTS)
	$(CC) $(LIBFLAGS) $(OBJECTS) $(LDFLAGS) -o $@
.c.o:
	$(CC) $(INCFLAGS) $(CFLAGS) -fPIC $< -o $@

run: $(BINARY)
	LD_LIBRARY_PATH=$(LIBPATHS) ./$(BINARY) $(table)


distclean: clean
	rm -f $(BINARY)

clean:
	rm -f $(OBJECTS) $(BINARY)
