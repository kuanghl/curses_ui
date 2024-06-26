# Makefile for PDCurses for X11

SHELL		= /bin/bash
THIS		= Makefile



PDCURSES_SRCDIR	= ..

osdir		= .
srcdir		= $(PDCURSES_SRCDIR)/pdcurses
demodir		= $(PDCURSES_SRCDIR)/demos

prefix		= /usr/local
exec_prefix	= ${prefix}
libdir		= ${exec_prefix}/lib
bindir		= ${exec_prefix}/bin
includedir	= ${prefix}/include

PDCURSES_CONFIG_H	=$(osdir)/config.h
PDCURSES_CURSES_H	=$(PDCURSES_SRCDIR)/curses.h
PDCURSES_CURSPRIV_H	=$(PDCURSES_SRCDIR)/curspriv.h
PDCURSES_HEADERS	=$(PDCURSES_CONFIG_H) $(PDCURSES_CURSES_H) \
$(PDCURSES_CURSPRIV_H)
PDCURSES_X11_H		=$(osdir)/pdcx11.h

SHLPRE		= lib
SHLPST		= .so
LD_RXLIB1	= gcc -shared
LD_RXLIB2	=   -L/usr/lib/x86_64-linux-gnu -lXaw -lXmu -lXt -lX11 -lXpm -lSM -lICE -lXext    -lc

CFLAGS		=  -O2 -Wall -Wextra -pedantic -Werror

CPPFLAGS	= -DHAVE_CONFIG_H -DXCURSES  -DPDC_WIDE -I$(PDCURSES_SRCDIR)

BUILD		= gcc -c $(CFLAGS) $(CPPFLAGS) -I/usr/include/X11 -I/usr/include
DYN_BUILD	=  $(BUILD) -fPIC -DDYNAMIC -o $@

LINK		= gcc
LDFLAGS		= $(LIBCURSES)     -L/usr/lib/x86_64-linux-gnu -lXaw -lXmu -lXt -lX11 -lXpm -lSM -lICE -lXext   

INSTALL		= $(osdir)/install-sh
RANLIB		= ranlib

LIBCURSES	= libXCurses.a

LIB_DEPS        = -L$(PDCURSES_SRCDIR)/x11 -lXCurses

PDCLIBS		= $(LIBCURSES)  libXCurses.so

DEMOS		= calendar firework init_col mbrot newtest ozdemo picsview \
ptest rain speed testcurs test_pan tuidemo widetest worm xmas
DEMOOBJS	= calendar.o firework.o init_col.o mbrot.o newtest.o ozdemo.o picsview.o \
ptest.o rain.o speed.o testcurs.o test_pan.o tui.o tuidemo.o widetest.o worm.o xmas.o

SHLFILE		= XCurses

all:	$(PDCLIBS)

install:
	$(INSTALL) -d -m 755 $(DESTDIR)$(libdir)
	$(INSTALL) -d -m 755 $(DESTDIR)$(bindir)
	$(INSTALL) -d -m 755 $(DESTDIR)$(includedir)
	$(INSTALL) -d -m 755 $(DESTDIR)$(includedir)/xcurses
	$(INSTALL) -c -m 644 $(PDCURSES_CURSES_H) \
		$(DESTDIR)$(includedir)/xcurses/curses.h
	$(INSTALL) -c -m 644 $(PDCURSES_SRCDIR)/panel.h \
		$(DESTDIR)$(includedir)/xcurses/panel.h
	$(INSTALL) -c -m 644 $(osdir)/libXCurses.a $(DESTDIR)$(libdir)/libXCurses.a
	-$(RANLIB) $(DESTDIR)$(libdir)/libXCurses.a
	-$(INSTALL) -c -m 755 $(osdir)/$(SHLPRE)$(SHLFILE)$(SHLPST) \
		$(DESTDIR)$(libdir)/$(SHLPRE)$(SHLFILE)$(SHLPST)
	$(INSTALL) -c -m 755 $(osdir)/xcurses-config $(DESTDIR)$(bindir)/xcurses-config

clean:
	-rm -rf *.o *.sho trace $(PDCLIBS) $(DEMOS) config.log \
		config.cache config.status

demos:	$(DEMOS)

distclean: clean
	-rm -f Makefile config.h xcurses-config

mostlyclean: clean

realclean: distclean

LIBOBJS = addch.o addchstr.o addstr.o attr.o beep.o bkgd.o border.o \
clear.o color.o delch.o deleteln.o getch.o getstr.o getyx.o \
inch.o inchstr.o initscr.o inopts.o insch.o insstr.o instr.o kernel.o \
keyname.o mouse.o move.o outopts.o overlay.o pad.o panel.o printw.o \
refresh.o scanw.o scr_dump.o scroll.o slk.o termattr.o terminfo.o \
touch.o util.o window.o debug.o

PDCOBJS = pdcclip.o pdcdisp.o pdcgetsc.o pdckbd.o pdcscrn.o pdcsetsc.o \
pdcutil.o sb.o scrlbox.o

LIBSHOBJS = $(LIBOBJS:.o=.sho)
PDCSHOBJS = $(PDCOBJS:.o=.sho)

SHOFILES = $(LIBSHOBJS) $(PDCSHOBJS)

$(LIBCURSES) : $(LIBOBJS) $(PDCOBJS)
	ar rv $@ $?
	-$(RANLIB) $@

$(SHLPRE)$(SHLFILE)$(SHLPST) : $(SHOFILES)
	$(LD_RXLIB1) -o $@ $(SHOFILES) $(LD_RXLIB2)

$(LIBOBJS) $(PDCOBJS) $(SHOFILES) : $(PDCURSES_HEADERS)
$(PDCOBJS) $(PDCSHOBJS) : $(PDCURSES_X11_H)
$(DEMOOBJS) : $(PDCURSES_CURSES_H)
$(DEMOS) : $(LIBCURSES)

addch.o: $(srcdir)/addch.c
	$(BUILD) $(srcdir)/addch.c

addchstr.o: $(srcdir)/addchstr.c
	$(BUILD) $(srcdir)/addchstr.c

addstr.o: $(srcdir)/addstr.c
	$(BUILD) $(srcdir)/addstr.c

attr.o: $(srcdir)/attr.c
	$(BUILD) $(srcdir)/attr.c

beep.o: $(srcdir)/beep.c
	$(BUILD) $(srcdir)/beep.c

bkgd.o: $(srcdir)/bkgd.c
	$(BUILD) $(srcdir)/bkgd.c

border.o: $(srcdir)/border.c
	$(BUILD) $(srcdir)/border.c

clear.o: $(srcdir)/clear.c
	$(BUILD) $(srcdir)/clear.c

color.o: $(srcdir)/color.c
	$(BUILD) $(srcdir)/color.c

delch.o: $(srcdir)/delch.c
	$(BUILD) $(srcdir)/delch.c

deleteln.o: $(srcdir)/deleteln.c
	$(BUILD) $(srcdir)/deleteln.c

getch.o: $(srcdir)/getch.c
	$(BUILD) $(srcdir)/getch.c

getstr.o: $(srcdir)/getstr.c
	$(BUILD) $(srcdir)/getstr.c

getyx.o: $(srcdir)/getyx.c
	$(BUILD) $(srcdir)/getyx.c

inch.o: $(srcdir)/inch.c
	$(BUILD) $(srcdir)/inch.c

inchstr.o: $(srcdir)/inchstr.c
	$(BUILD) $(srcdir)/inchstr.c

initscr.o: $(srcdir)/initscr.c
	$(BUILD) $(srcdir)/initscr.c

inopts.o: $(srcdir)/inopts.c
	$(BUILD) $(srcdir)/inopts.c

insch.o: $(srcdir)/insch.c
	$(BUILD) $(srcdir)/insch.c

insstr.o: $(srcdir)/insstr.c
	$(BUILD) $(srcdir)/insstr.c

instr.o: $(srcdir)/instr.c
	$(BUILD) $(srcdir)/instr.c

kernel.o: $(srcdir)/kernel.c
	$(BUILD) $(srcdir)/kernel.c

keyname.o: $(srcdir)/keyname.c
	$(BUILD) $(srcdir)/keyname.c

mouse.o: $(srcdir)/mouse.c
	$(BUILD) $(srcdir)/mouse.c

move.o: $(srcdir)/move.c
	$(BUILD) $(srcdir)/move.c

outopts.o: $(srcdir)/outopts.c
	$(BUILD) $(srcdir)/outopts.c

overlay.o: $(srcdir)/overlay.c
	$(BUILD) $(srcdir)/overlay.c

pad.o: $(srcdir)/pad.c
	$(BUILD) $(srcdir)/pad.c

panel.o: $(srcdir)/panel.c $(PDCURSES_SRCDIR)/panel.h
	$(BUILD) $(srcdir)/panel.c

printw.o: $(srcdir)/printw.c
	$(BUILD) $(srcdir)/printw.c

refresh.o: $(srcdir)/refresh.c
	$(BUILD) $(srcdir)/refresh.c

scanw.o: $(srcdir)/scanw.c
	$(BUILD) $(srcdir)/scanw.c

scr_dump.o: $(srcdir)/scr_dump.c
	$(BUILD) $(srcdir)/scr_dump.c

scroll.o: $(srcdir)/scroll.c
	$(BUILD) $(srcdir)/scroll.c

slk.o: $(srcdir)/slk.c
	$(BUILD) $(srcdir)/slk.c

termattr.o: $(srcdir)/termattr.c
	$(BUILD) $(srcdir)/termattr.c

terminfo.o: $(srcdir)/terminfo.c
	$(BUILD) $(srcdir)/terminfo.c

touch.o: $(srcdir)/touch.c
	$(BUILD) $(srcdir)/touch.c

util.o: $(srcdir)/util.c
	$(BUILD) $(srcdir)/util.c

window.o: $(srcdir)/window.c
	$(BUILD) $(srcdir)/window.c

debug.o: $(srcdir)/debug.c
	$(BUILD) $(srcdir)/debug.c

pdcclip.o: $(osdir)/pdcclip.c
	$(BUILD) $(osdir)/pdcclip.c

pdcdisp.o: $(osdir)/pdcdisp.c
	$(BUILD) $(osdir)/pdcdisp.c

pdcgetsc.o: $(osdir)/pdcgetsc.c
	$(BUILD) $(osdir)/pdcgetsc.c

pdckbd.o: $(osdir)/pdckbd.c
	$(BUILD) $(osdir)/pdckbd.c

pdcscrn.o: $(osdir)/pdcscrn.c
	$(BUILD) $(osdir)/pdcscrn.c

pdcsetsc.o: $(osdir)/pdcsetsc.c
	$(BUILD) $(osdir)/pdcsetsc.c

pdcutil.o: $(osdir)/pdcutil.c
	$(BUILD) $(osdir)/pdcutil.c

scrlbox.o: $(osdir)/scrlbox.c
	$(BUILD) $(osdir)/scrlbox.c

sb.o: $(osdir)/sb.c
	$(BUILD) $(osdir)/sb.c

addch.sho: $(srcdir)/addch.c
	$(DYN_BUILD) $(srcdir)/addch.c
	

addchstr.sho: $(srcdir)/addchstr.c
	$(DYN_BUILD) $(srcdir)/addchstr.c
	

addstr.sho: $(srcdir)/addstr.c
	$(DYN_BUILD) $(srcdir)/addstr.c
	

attr.sho: $(srcdir)/attr.c
	$(DYN_BUILD) $(srcdir)/attr.c
	

beep.sho: $(srcdir)/beep.c
	$(DYN_BUILD) $(srcdir)/beep.c
	

bkgd.sho: $(srcdir)/bkgd.c
	$(DYN_BUILD) $(srcdir)/bkgd.c
	

border.sho: $(srcdir)/border.c
	$(DYN_BUILD) $(srcdir)/border.c
	

clear.sho: $(srcdir)/clear.c
	$(DYN_BUILD) $(srcdir)/clear.c
	

color.sho: $(srcdir)/color.c
	$(DYN_BUILD) $(srcdir)/color.c
	

delch.sho: $(srcdir)/delch.c
	$(DYN_BUILD) $(srcdir)/delch.c
	

deleteln.sho: $(srcdir)/deleteln.c
	$(DYN_BUILD) $(srcdir)/deleteln.c
	

getch.sho: $(srcdir)/getch.c
	$(DYN_BUILD) $(srcdir)/getch.c
	

getstr.sho: $(srcdir)/getstr.c
	$(DYN_BUILD) $(srcdir)/getstr.c
	

getyx.sho: $(srcdir)/getyx.c
	$(DYN_BUILD) $(srcdir)/getyx.c
	

inch.sho: $(srcdir)/inch.c
	$(DYN_BUILD) $(srcdir)/inch.c
	

inchstr.sho: $(srcdir)/inchstr.c
	$(DYN_BUILD) $(srcdir)/inchstr.c
	

initscr.sho: $(srcdir)/initscr.c
	$(DYN_BUILD) $(srcdir)/initscr.c
	

inopts.sho: $(srcdir)/inopts.c
	$(DYN_BUILD) $(srcdir)/inopts.c
	

insch.sho: $(srcdir)/insch.c
	$(DYN_BUILD) $(srcdir)/insch.c
	

insstr.sho: $(srcdir)/insstr.c
	$(DYN_BUILD) $(srcdir)/insstr.c
	

instr.sho: $(srcdir)/instr.c
	$(DYN_BUILD) $(srcdir)/instr.c
	

kernel.sho: $(srcdir)/kernel.c
	$(DYN_BUILD) $(srcdir)/kernel.c
	

keyname.sho: $(srcdir)/keyname.c
	$(DYN_BUILD) $(srcdir)/keyname.c
	

mouse.sho: $(srcdir)/mouse.c
	$(DYN_BUILD) $(srcdir)/mouse.c
	

move.sho: $(srcdir)/move.c
	$(DYN_BUILD) $(srcdir)/move.c
	

outopts.sho: $(srcdir)/outopts.c
	$(DYN_BUILD) $(srcdir)/outopts.c
	

overlay.sho: $(srcdir)/overlay.c
	$(DYN_BUILD) $(srcdir)/overlay.c
	

pad.sho: $(srcdir)/pad.c
	$(DYN_BUILD) $(srcdir)/pad.c
	

panel.sho: $(srcdir)/panel.c $(PDCURSES_SRCDIR)/panel.h
	$(DYN_BUILD) $(srcdir)/panel.c
	

printw.sho: $(srcdir)/printw.c
	$(DYN_BUILD) $(srcdir)/printw.c
	

refresh.sho: $(srcdir)/refresh.c
	$(DYN_BUILD) $(srcdir)/refresh.c
	

scanw.sho: $(srcdir)/scanw.c
	$(DYN_BUILD) $(srcdir)/scanw.c
	

scr_dump.sho: $(srcdir)/scr_dump.c
	$(DYN_BUILD) $(srcdir)/scr_dump.c
	

scroll.sho: $(srcdir)/scroll.c
	$(DYN_BUILD) $(srcdir)/scroll.c
	

slk.sho: $(srcdir)/slk.c
	$(DYN_BUILD) $(srcdir)/slk.c
	

termattr.sho: $(srcdir)/termattr.c
	$(DYN_BUILD) $(srcdir)/termattr.c
	

terminfo.sho: $(srcdir)/terminfo.c
	$(DYN_BUILD) $(srcdir)/terminfo.c
	

touch.sho: $(srcdir)/touch.c
	$(DYN_BUILD) $(srcdir)/touch.c
	

util.sho: $(srcdir)/util.c
	$(DYN_BUILD) $(srcdir)/util.c
	

window.sho: $(srcdir)/window.c
	$(DYN_BUILD) $(srcdir)/window.c
	

debug.sho: $(srcdir)/debug.c
	$(DYN_BUILD) $(srcdir)/debug.c
	

pdcclip.sho: $(osdir)/pdcclip.c
	$(DYN_BUILD) $(osdir)/pdcclip.c
	

pdcdisp.sho: $(osdir)/pdcdisp.c
	$(DYN_BUILD) $(osdir)/pdcdisp.c
	

pdcgetsc.sho: $(osdir)/pdcgetsc.c
	$(DYN_BUILD) $(osdir)/pdcgetsc.c
	

pdckbd.sho: $(osdir)/pdckbd.c
	$(DYN_BUILD) $(osdir)/pdckbd.c
	

pdcscrn.sho: $(osdir)/pdcscrn.c
	$(DYN_BUILD) $(osdir)/pdcscrn.c
	

pdcsetsc.sho: $(osdir)/pdcsetsc.c
	$(DYN_BUILD) $(osdir)/pdcsetsc.c
	

pdcutil.sho: $(osdir)/pdcutil.c
	$(DYN_BUILD) $(osdir)/pdcutil.c
	

scrlbox.sho: $(osdir)/scrlbox.c
	$(DYN_BUILD) $(osdir)/scrlbox.c
	

sb.sho: $(osdir)/sb.c
	$(DYN_BUILD) $(osdir)/sb.c
	

calendar: calendar.o
	$(LINK) calendar.o -o $@ $(LDFLAGS)

firework: firework.o
	$(LINK) firework.o -o $@ $(LDFLAGS)

init_col: init_col.o
	$(LINK) init_col.o -o $@ $(LDFLAGS)

mbrot: mbrot.o
	$(LINK) mbrot.o -o $@ $(LDFLAGS)

newtest: newtest.o
	$(LINK) newtest.o -o $@ $(LDFLAGS)

ozdemo: ozdemo.o
	$(LINK) ozdemo.o -o $@ $(LDFLAGS)

picsview: picsview.o
	$(LINK) picsview.o -o $@ $(LDFLAGS)

ptest: ptest.o
	$(LINK) ptest.o -o $@ $(LDFLAGS)

rain: rain.o
	$(LINK) rain.o -o $@ $(LDFLAGS)

speed: speed.o
	$(LINK) speed.o -o $@ $(LDFLAGS)

testcurs: testcurs.o
	$(LINK) testcurs.o -o $@ $(LDFLAGS)

test_pan: test_pan.o
	$(LINK) test_pan.o -o $@ $(LDFLAGS)

tuidemo: tuidemo.o tui.o
	$(LINK) tui.o tuidemo.o -o $@ $(LDFLAGS)

widetest: widetest.o
	$(LINK) widetest.o -o $@ $(LDFLAGS)

worm: worm.o
	$(LINK) worm.o -o $@ $(LDFLAGS)

xmas: xmas.o
	$(LINK) xmas.o -o $@ $(LDFLAGS)

calendar.o: $(demodir)/calendar.c
	$(BUILD) $(demodir)/calendar.c

firework.o: $(demodir)/firework.c
	$(BUILD) $(demodir)/firework.c

init_col.o: $(demodir)/init_col.c
	$(BUILD) $(demodir)/init_col.c

mbrot.o: $(demodir)/mbrot.c
	$(BUILD) $(demodir)/mbrot.c

newtest.o: $(demodir)/newtest.c
	$(BUILD) $(demodir)/newtest.c

ozdemo.o: $(demodir)/ozdemo.c
	$(BUILD) $(demodir)/ozdemo.c

picsview.o: $(demodir)/picsview.c
	$(BUILD) $(demodir)/picsview.c

ptest.o: $(demodir)/ptest.c $(PDCURSES_SRCDIR)/panel.h
	$(BUILD) $(demodir)/ptest.c

rain.o: $(demodir)/rain.c
	$(BUILD) $(demodir)/rain.c

speed.o: $(demodir)/speed.c
	$(BUILD) $(demodir)/speed.c

testcurs.o: $(demodir)/testcurs.c
	$(BUILD) $(demodir)/testcurs.c

test_pan.o: $(demodir)/test_pan.c $(PDCURSES_SRCDIR)/panel.h
	$(BUILD) $(demodir)/test_pan.c

tui.o: $(demodir)/tui.c $(demodir)/tui.h
	$(BUILD) $(demodir)/tui.c

tuidemo.o: $(demodir)/tuidemo.c
	$(BUILD) $(demodir)/tuidemo.c

widetest.o: $(demodir)/widetest.c
	$(BUILD) $(demodir)/widetest.c

worm.o: $(demodir)/worm.c
	$(BUILD) $(demodir)/worm.c

xmas.o: $(demodir)/xmas.c
	$(BUILD) $(demodir)/xmas.c

# This section provides for compiling and linking the
# ncurses test programs.

ncurses_testdir	= $(HOME)/ncurses-6.4/test

NCURSES_TESTS	= back_ground background blue \
bs cardfile chgat clip_printw color_content \
color_set demo_altkeys demo_defkey demo_forms \
demo_keyok demo_menus demo_new_pair  \
demo_panels demo_termcap demo_terminfo ditto \
dots dots_curses dots_mvcur dots_termcap \
dots_xcurses dup_field echochar  extended_color \
filter firstlast foldkeys form_driver_w gdc \
hanoi hashtest inchs inch_wide insdelln \
inserts ins_wide key_names keynames knight \
list_keys lrtest move_field \
movewindow ncurses newdemo padview pair_content \
picsmap railroad redraw savescreen sp_tinfo \
tclock testaddch test_addchstr test_addstr \
test_add_wchstr test_addwstr\
test_arrays test_getstr test_get_wstr test_instr \
test_opaque testscanw test_setupterm test_sgr test_termattrs \
test_tparm test_vid_puts test_vidputs view

ncurses_tests: $(NCURSES_TESTS)

ncurses_clean:
	-rm -f *.o trace $(NCURSES_TESTS)

NCFLAGS		= -I$(demodir) -I$(ncurses_testdir)

back_ground: back_ground.o dump_window.o $(LIBCURSES)
	$(LINK) back_ground.o dump_window.o -o $@ $(LDFLAGS)

background: background.o dump_window.o $(LIBCURSES)
	$(LINK) background.o dump_window.o -o $@ $(LDFLAGS)

blue: blue.o $(LIBCURSES)
	$(LINK) blue.o -o $@ $(LDFLAGS)

bs: bs.o $(LIBCURSES)
	$(LINK) bs.o -o $@ $(LDFLAGS)

cardfile: cardfile.o $(LIBCURSES)
	$(LINK) cardfile.o -o $@ $(LDFLAGS)

chgat: chgat.o popup_msg.o $(LIBCURSES)
	$(LINK) chgat.o popup_msg.o -o $@ $(LDFLAGS)

clip_printw: clip_printw.o popup_msg.o $(LIBCURSES)
	$(LINK) clip_printw.o popup_msg.o -o $@ $(LDFLAGS)

color_content: color_content.o $(LIBCURSES)
	$(LINK) color_content.o -o $@ $(LDFLAGS)

color_set: color_set.o $(LIBCURSES)
	$(LINK) color_set.o -o $@ $(LDFLAGS)

demo_altkeys: demo_altkeys.o $(LIBCURSES)
	$(LINK) demo_altkeys.o -o $@ $(LDFLAGS)

demo_defkey: demo_defkey.o popup_msg.o $(LIBCURSES)
	$(LINK) demo_defkey.o popup_msg.o -o $@ $(LDFLAGS)

demo_forms: demo_forms.o $(LIBCURSES)
	$(LINK) demo_forms.o -o $@ $(LDFLAGS)

demo_keyok: demo_keyok.o $(LIBCURSES)
	$(LINK) demo_keyok.o -o $@ $(LDFLAGS)

demo_menus: demo_menus.o $(LIBCURSES)
	$(LINK) demo_menus.o -o $@ $(LDFLAGS)

demo_new_pair: demo_new_pair.o popup_msg.o terminfo.o $(LIBCURSES)
	$(LINK) demo_new_pair.o popup_msg.o terminfo.o -o $@ $(LDFLAGS)

demo_panels: demo_panels.o $(LIBCURSES)
	$(LINK) demo_panels.o -o $@ $(LDFLAGS)

demo_tabs: demo_tabs.o $(LIBCURSES)
	$(LINK) demo_tabs.o -o $@ $(LDFLAGS)

demo_termcap: demo_termcap.o $(LIBCURSES)
	$(LINK) demo_termcap.o -o $@ $(LDFLAGS)

demo_terminfo: demo_terminfo.o $(LIBCURSES)
	$(LINK) demo_terminfo.o -o $@ $(LDFLAGS)

ditto: ditto.o $(LIBCURSES)
	$(LINK) ditto.o -o $@ $(LDFLAGS)

dots: dots.o $(LIBCURSES)
	$(LINK) dots.o -o $@ $(LDFLAGS)

dots_curses: dots_curses.o $(LIBCURSES)
	$(LINK) dots_curses.o -o $@ $(LDFLAGS)

dots_mvcur: dots_mvcur.o $(LIBCURSES)
	$(LINK) dots_mvcur.o -o $@ $(LDFLAGS)

dots_termcap: dots_termcap.o $(LIBCURSES)
	$(LINK) dots_termcap.o -o $@ $(LDFLAGS)

dots_xcurses: dots_xcurses.o $(LIBCURSES)
	$(LINK) dots_xcurses.o -o $@ $(LDFLAGS)

dup_field: dup_field.o $(LIBCURSES)
	$(LINK) dup_field.o -o $@ $(LDFLAGS)

echochar: echochar.o $(LIBCURSES)
	$(LINK) echochar.o -o $@ $(LDFLAGS)

extended_color: extended_color.o $(LIBCURSES)
	$(LINK) extended_color.o -o $@ $(LDFLAGS)

filter: filter.o popup_msg.o $(LIBCURSES)
	$(LINK) filter.o popup_msg.o -o $@ $(LDFLAGS)

firstlast: firstlast.o $(LIBCURSES)
	$(LINK) firstlast.o -o $@ $(LDFLAGS)

foldkeys: foldkeys.o $(LIBCURSES)
	$(LINK) foldkeys.o -o $@ $(LDFLAGS)

form_driver_w: form_driver_w.o $(LIBCURSES)
	$(LINK) form_driver_w.o -o $@ $(LDFLAGS)

gdc: gdc.o $(LIBCURSES)
	$(LINK) gdc.o -o $@ $(LDFLAGS)

hanoi: hanoi.o $(LIBCURSES)
	$(LINK) hanoi.o -o $@ $(LDFLAGS) -lm

hashtest: hashtest.o $(LIBCURSES)
	$(LINK) hashtest.o -o $@ $(LDFLAGS)

inchs: inchs.o popup_msg.o $(LIBCURSES)
	$(LINK) inchs.o popup_msg.o -o $@ $(LDFLAGS)

inch_wide: inch_wide.o popup_msg.o $(LIBCURSES)
	$(LINK) inch_wide.o popup_msg.o -o $@ $(LDFLAGS)

insdelln: insdelln.o $(LIBCURSES)
	$(LINK) insdelln.o -o $@ $(LDFLAGS)

inserts: inserts.o $(LIBCURSES)
	$(LINK) inserts.o -o $@ $(LDFLAGS)

ins_wide: ins_wide.o $(LIBCURSES)
	$(LINK) ins_wide.o -o $@ $(LDFLAGS)

key_names: key_names.o $(LIBCURSES)
	$(LINK) key_names.o -o $@ $(LDFLAGS)

keynames: keynames.o $(LIBCURSES)
	$(LINK) keynames.o -o $@ $(LDFLAGS)

knight: knight.o $(LIBCURSES)
	$(LINK) knight.o -o $@ $(LDFLAGS)

list_keys: list_keys.o $(LIBCURSES)
	$(LINK) list_keys.o -o $@ $(LDFLAGS)

lrtest: lrtest.o $(LIBCURSES)
	$(LINK) lrtest.o -o $@ $(LDFLAGS)

move_field: move_field.o $(LIBCURSES)
	$(LINK) move_field.o -o $@ $(LDFLAGS)

movewindow: movewindow.o $(LIBCURSES)
	$(LINK) movewindow.o -o $@ $(LDFLAGS)

ncurses: ncurses.o $(LIBCURSES)
	$(LINK) ncurses.o -o $@ $(LDFLAGS)

newdemo: newdemo.o $(LIBCURSES)
	$(LINK) newdemo.o -o $@ $(LDFLAGS)

padview: padview.o popup_msg.o $(LIBCURSES)
	$(LINK) padview.o popup_msg.o -o $@ $(LDFLAGS)

pair_content: pair_content.o $(LIBCURSES)
	$(LINK) pair_content.o -o $@ $(LDFLAGS)

picsmap: picsmap.o $(LIBCURSES)
	$(LINK) picsmap.o -o $@ $(LDFLAGS)

railroad: railroad.o $(LIBCURSES)
	$(LINK) railroad.o -o $@ $(LDFLAGS)

redraw: redraw.o popup_msg.o $(LIBCURSES)
	$(LINK) redraw.o popup_msg.o -o $@ $(LDFLAGS)

savescreen: savescreen.o $(LIBCURSES)
	$(LINK) savescreen.o -o $@ $(LDFLAGS)

sp_tinfo: sp_tinfo.o $(LIBCURSES)
	$(LINK) sp_tinfo.o -o $@ $(LDFLAGS)

tclock: tclock.o $(LIBCURSES)
	$(LINK) tclock.o -o $@ $(LDFLAGS) -lm

testaddch: testaddch.o $(LIBCURSES)
	$(LINK) testaddch.o -o $@ $(LDFLAGS)

test_addchstr: test_addchstr.o $(LIBCURSES)
	$(LINK) test_addchstr.o -o $@ $(LDFLAGS)

test_addstr: test_addstr.o $(LIBCURSES)
	$(LINK) test_addstr.o -o $@ $(LDFLAGS)

test_add_wchstr: test_add_wchstr.o $(LIBCURSES)
	$(LINK) test_add_wchstr.o -o $@ $(LDFLAGS)

test_addwstr: test_addwstr.o $(LIBCURSES)
	$(LINK) test_addwstr.o -o $@ $(LDFLAGS)

test_arrays: test_arrays.o $(LIBCURSES)
	$(LINK) test_arrays.o -o $@ $(LDFLAGS)

test_getstr: test_getstr.o popup_msg.o $(LIBCURSES)
	$(LINK) test_getstr.o popup_msg.o -o $@ $(LDFLAGS)

test_get_wstr: test_get_wstr.o popup_msg.o $(LIBCURSES)
	$(LINK) test_get_wstr.o popup_msg.o -o $@ $(LDFLAGS)

test_instr: test_instr.o popup_msg.o $(LIBCURSES)
	$(LINK) test_instr.o popup_msg.o -o $@ $(LDFLAGS)

test_opaque: test_opaque.o $(LIBCURSES)
	$(LINK) test_opaque.o -o $@ $(LDFLAGS)

testscanw: testscanw.o $(LIBCURSES)
	$(LINK) testscanw.o -o $@ $(LDFLAGS)

test_setupterm: test_setupterm.o $(LIBCURSES)
	$(LINK) test_setupterm.o -o $@ $(LDFLAGS)

test_sgr: test_sgr.o $(LIBCURSES)
	$(LINK) test_sgr.o -o $@ $(LDFLAGS)

test_termattrs: test_termattrs.o $(LIBCURSES)
	$(LINK) test_termattrs.o -o $@ $(LDFLAGS)

test_tparm: test_tparm.o $(LIBCURSES)
	$(LINK) test_tparm.o -o $@ $(LDFLAGS)

test_vid_puts: test_vid_puts.o $(LIBCURSES)
	$(LINK) test_vid_puts.o -o $@ $(LDFLAGS)

test_vidputs: test_vidputs.o $(LIBCURSES)
	$(LINK) test_vidputs.o -o $@ $(LDFLAGS)

view: view.o popup_msg.o $(LIBCURSES)
	$(LINK) view.o popup_msg.o -o $@ $(LDFLAGS)

back_ground.o: $(ncurses_testdir)/back_ground.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/back_ground.c

background.o: $(ncurses_testdir)/background.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/background.c

blue.o: $(ncurses_testdir)/blue.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/blue.c

bs.o: $(ncurses_testdir)/bs.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/bs.c

cardfile.o: $(ncurses_testdir)/cardfile.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/cardfile.c

chgat.o: $(ncurses_testdir)/chgat.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/chgat.c

clip_printw.o: $(ncurses_testdir)/clip_printw.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/clip_printw.c

dump_window.o: $(ncurses_testdir)/dump_window.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/dump_window.c

color_content.o: $(ncurses_testdir)/color_content.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/color_content.c

color_set.o: $(ncurses_testdir)/color_set.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/color_set.c

demo_altkeys.o: $(ncurses_testdir)/demo_altkeys.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_altkeys.c

demo_defkey.o: $(ncurses_testdir)/demo_defkey.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_defkey.c

demo_forms.o: $(ncurses_testdir)/demo_forms.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_forms.c

demo_keyok.o: $(ncurses_testdir)/demo_keyok.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_keyok.c

demo_menus.o: $(ncurses_testdir)/demo_menus.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_menus.c

demo_new_pair.o: $(ncurses_testdir)/demo_new_pair.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_new_pair.c

demo_panels.o: $(ncurses_testdir)/demo_panels.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_panels.c

demo_termcap.o: $(ncurses_testdir)/demo_termcap.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_termcap.c

demo_terminfo.o: $(ncurses_testdir)/demo_terminfo.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/demo_terminfo.c

ditto.o: $(ncurses_testdir)/ditto.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/ditto.c

dots.o: $(ncurses_testdir)/dots.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/dots.c

dots_curses.o: $(ncurses_testdir)/dots_curses.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/dots_curses.c

dots_mvcur.o: $(ncurses_testdir)/dots_mvcur.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/dots_mvcur.c

dots_termcap.o: $(ncurses_testdir)/dots_termcap.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/dots_termcap.c

dots_xcurses.o: $(ncurses_testdir)/dots_xcurses.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/dots_xcurses.c

dup_field.o: $(ncurses_testdir)/dup_field.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/dup_field.c

echochar.o: $(ncurses_testdir)/echochar.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/echochar.c

extended_color.o: $(ncurses_testdir)/extended_color.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/extended_color.c

filter.o: $(ncurses_testdir)/filter.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/filter.c

firstlast.o: $(ncurses_testdir)/firstlast.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/firstlast.c

foldkeys.o: $(ncurses_testdir)/foldkeys.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/foldkeys.c

form_driver_w.o: $(ncurses_testdir)/form_driver_w.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/form_driver_w.c

gdc.o: $(ncurses_testdir)/gdc.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/gdc.c

hanoi.o: $(ncurses_testdir)/hanoi.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/hanoi.c

hashtest.o: $(ncurses_testdir)/hashtest.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/hashtest.c

inchs.o: $(ncurses_testdir)/inchs.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/inchs.c

inch_wide.o: $(ncurses_testdir)/inch_wide.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/inch_wide.c

insdelln.o: $(ncurses_testdir)/insdelln.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/insdelln.c

inserts.o: $(ncurses_testdir)/inserts.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/inserts.c

ins_wide.o: $(ncurses_testdir)/ins_wide.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/ins_wide.c

key_names.o: $(ncurses_testdir)/key_names.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/key_names.c

keynames.o: $(ncurses_testdir)/keynames.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/keynames.c

knight.o: $(ncurses_testdir)/knight.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/knight.c

list_keys.o: $(ncurses_testdir)/list_keys.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/list_keys.c

lrtest.o: $(ncurses_testdir)/lrtest.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/lrtest.c

move_field.o: $(ncurses_testdir)/move_field.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/move_field.c

movewindow.o: $(ncurses_testdir)/movewindow.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/movewindow.c

ncurses.o: $(ncurses_testdir)/ncurses.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/ncurses.c

newdemo.o: $(ncurses_testdir)/newdemo.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/newdemo.c

padview.o: $(ncurses_testdir)/padview.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/padview.c

pair_content.o: $(ncurses_testdir)/pair_content.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/pair_content.c

picsmap.o: $(ncurses_testdir)/picsmap.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/picsmap.c

popup_msg.o: $(ncurses_testdir)/popup_msg.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/popup_msg.c

railroad.o: $(ncurses_testdir)/railroad.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/railroad.c

redraw.o: $(ncurses_testdir)/redraw.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/redraw.c

savescreen.o: $(ncurses_testdir)/savescreen.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/savescreen.c

sp_tinfo.o: $(ncurses_testdir)/sp_tinfo.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/sp_tinfo.c

tclock.o: $(ncurses_testdir)/tclock.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/tclock.c

testaddch.o: $(ncurses_testdir)/testaddch.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/testaddch.c

test_addchstr.o: $(ncurses_testdir)/test_addchstr.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_addchstr.c

test_addstr.o: $(ncurses_testdir)/test_addstr.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_addstr.c

test_add_wchstr.o: $(ncurses_testdir)/test_add_wchstr.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_add_wchstr.c

test_addwstr.o: $(ncurses_testdir)/test_addwstr.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_addwstr.c

test_arrays.o: $(ncurses_testdir)/test_arrays.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_arrays.c

test_getstr.o: $(ncurses_testdir)/test_getstr.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_getstr.c

test_get_wstr.o: $(ncurses_testdir)/test_get_wstr.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_get_wstr.c

test_instr.o: $(ncurses_testdir)/test_instr.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_instr.c

test_opaque.o: $(ncurses_testdir)/test_opaque.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_opaque.c

testscanw.o: $(ncurses_testdir)/testscanw.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/testscanw.c

test_setupterm.o: $(ncurses_testdir)/test_setupterm.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_setupterm.c

test_sgr.o: $(ncurses_testdir)/test_sgr.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_sgr.c

test_termattrs.o: $(ncurses_testdir)/test_termattrs.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_termattrs.c

test_tparm.o: $(ncurses_testdir)/test_tparm.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_tparm.c

test_vid_puts.o: $(ncurses_testdir)/test_vid_puts.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_vid_puts.c

test_vidputs.o: $(ncurses_testdir)/test_vidputs.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/test_vidputs.c

view.o: $(ncurses_testdir)/view.c $(PDCURSES_CURSES_H)
	$(BUILD) $(NCFLAGS) $(ncurses_testdir)/view.c

