MCU=ATMEGA32U2
#MCU=ATMEGA32U4

CFLAGS = -Os -D${MCU} -DF_CPU=16000000UL -mmcu=${MCU} -Ilib 
SOURCES = lib/usb_srs_vendor_v1_2.c main.c
TARGET = usb_hello

all:
	avr-gcc -o ${TARGET}.elf ${SOURCES} ${CFLAGS}
	avr-objcopy -O ihex -R .signature -R .fuse -R .eeprom ${TARGET}.elf ${TARGET}.hex

flash: all
	dfu-programmer ${MCU} erase
	dfu-programmer ${MCU} flash ${TARGET}.hex
	dfu-programmer ${MCU} reset

clean:
	rm -rf *.hex *.elf
