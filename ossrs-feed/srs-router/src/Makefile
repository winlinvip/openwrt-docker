.PHONY: all router porting verify helloworld st clean

all: porting st verify helloworld #router

router: ./srs-router st porting

CFLAGS=-Istate-threads/obj
LDLIBS=state-threads/obj/libst.a

./srs-router: main.c
	$(CC) $(CPPFLAGS) $(CFLAGS) $(LDFLAGS) -Wall -o $@ $^ $(LDLIBS)

st:
	cd state-threads && $(MAKE) linux-debug

porting:
	cd state-threads/tools/porting && $(MAKE)

verify: st
	cd state-threads/tools/verify && $(MAKE)

helloworld: st
	cd state-threads/tools/helloworld && $(MAKE)

clean:
	cd state-threads && $(MAKE) clean
	cd state-threads/tools/porting && $(MAKE) clean
	cd state-threads/tools/verify && $(MAKE) clean
	cd state-threads/tools/helloworld && $(MAKE) clean
	rm -f srs-router

