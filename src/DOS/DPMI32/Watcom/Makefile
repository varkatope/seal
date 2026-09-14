# Makefile for WATCOM C/C++32 10.0 (DOS4GW protected mode, flat memory model)

.EXTENSIONS:
.EXTENSIONS:.exe 
.EXTENSIONS:.obj 
.EXTENSIONS:.c .asm .h

CC = wcc386
LD = wlink
AR = wlib -s -t -q -n
CFLAGS = -zq -zu -w9 -we -5r -s -oxt -D__DPMI__ -D__ASM__
LFLAGS = system dos4g

AS = wasm
AFLAGS = -zq -w9 -we -5r

#AS = tasm
#AFLAGS = -t -m -q -ml -zi

OBJS = audio.obj wavfile.obj xmfile.obj s3mfile.obj modfile.obj mtmfile.obj &
	iofile.obj modeng.obj nondrv.obj mixdrv.obj _mixdrv.obj msdos.obj &
	sbdrv.obj awedrv.obj pasdrv.obj wssdrv.obj gusdrv.obj ariadrv.obj

LIB = "..\lib\DOS\audiowcf.lib"

all : $(LIB) mp.exe .SYMBOLIC
	@echo done.

mp.exe : mp.obj $(LIB)
	$(LD) $(LFLAGS) file mp.obj library ..\lib\DOS\audiowcf.lib

$(LIB) : $(OBJS)
	%create audiowcf.lnk
	for %i in ($(OBJS)) do @%append audiowcf.lnk %i
	$(AR) $(LIB) @audiowcf.lnk
	@del audiowcf.lnk

.c.obj :
	$(CC) $(CFLAGS) $<

.asm.obj :
	$(AS) $(AFLAGS) $<

clean : .SYMBOLIC
	@del *.obj
