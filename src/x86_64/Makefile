CC = x86_64-w64-mingw32-gcc
CFLAGS =  -ffreestanding -I/usr/include/efi -I/usr/include/efi/x86_64 -I/usr/include/efi/protocol

OBJECTS = hello.o \
	  gnu-efi-3.0.9/data.o

all: kernel fatimage hdimage

kernel: $(OBJECTS)
	$(CC) -nostdlib -Wl,-dll -shared -Wl,--subsystem,10 -e efi_main -o BOOTX64.EFI $(OBJECTS) -lgcc

%.o: %.c
	$(CC) -c $< -o $@ $(CFLAGS)

fatimage:
	dd if=/dev/zero of=fat.img bs=1k count=1440
	mformat -i fat.img -f 1440 ::
	mmd -i fat.img ::/EFI
	mmd -i fat.img ::/EFI/BOOT
	mcopy -i fat.img BOOTX64.EFI ::/EFI/BOOT

hdimage:
	mkgpt -o hdimage.bin --image-size 4096 --part fat.img --type system

qemu:
	qemu-system-x86_64 -L /usr/share/ovmf/ -bios OVMF.fd -drive file=hdimage.bin,format=raw

clean:
	$(RM) $(OBJECTS)
	$(RM) BOOTX64.EFI
	$(RM) fat.img
	$(RM) hdimage.bin
