# Einherjar-OS - ᛖᛁᚾᚺᛖᚱᛃᚨᚱ
Desktop OS

Packages to install on a Debian-based Linux distros
===================================================

sudo apt install qemu binutils-mingw-w64 gcc-mingw-w64 xorriso mtools

Other tools to install are:
--------------------------

mkgpt:
	wget http://www.tysos.org/files/efi/mkgpt-latest.tar.bz2
	tar jxf mkgpt-latest.tar.bz2
	cd mkgpt && ./configure && make && sudo make install && cd ..

gnu-efi:
	https://sourceforge.net/projects/gnu-efi/
