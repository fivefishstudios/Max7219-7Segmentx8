

VER_H=../include/bearssl/bearssl_git.h

all T0 clean: bearssl/README.txt
	PATH=$(PATH):$(PWD)/../../xtensa-lx106-elf/bin/ && cd bearssl && make CONF=esp8266 $@

install: all version-header
	cp bearssl/esp8266/libbearssl.a ../lib/.
	cp bearssl/inc/bearssl*.h ../include/bearssl/.

bearssl/README.txt:
	git submodule update --init --recursive bearssl
	cd bearssl && (git remote add bearssl https://www.bearssl.org/git/BearSSL || true)

merge-upstream:
	cd bearssl && git pull bearssl master

version-header:
	echo "// Do not edit -- Automatically generated by tools/sdk/ssl/bearssl/Makefile" > $(VER_H)
	echo -n "#define BEARSSL_GIT " >> $(VER_H)
	cd bearssl && git rev-parse --short HEAD >> ../$(VER_H)

native: bearssl/README.txt
	cd bearssl && make

native32: bearssl/README.txt
	cd bearssl && make CONF=Unix32
