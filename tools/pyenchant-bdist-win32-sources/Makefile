#
#  Makefile for building pyenchant win32 dependencies.
#
BUILD_DIR = $(PWD)/build
ENCHANT_DIR = enchant-1.6.0

ENCHANT_CONFIG_OPTS = --enable-ispell --enable-myspell --disable-aspell --disable-dependency-tracking --disable-maintainer-mode --with-pic
CC = gcc
CXX = g++
ENCHANT_CFLAGS = -I$(BUILD_DIR)/include/glib-2.0 -static-libgcc -static-libstdc++
#ENCHANT_LIBS = -L$(BUILD_DIR)/lib -lglib-2.0 -lgmodule-2.0

all: $(BUILD_DIR)/lib/libenchant.dll $(BUILD_DIR)/share/enchant/myspell/en_GB.dic \
	$(BUILD_DIR)/share/enchant/myspell/en_US.dic $(BUILD_DIR)/share/enchant/myspell/de_DE.dic \
	$(BUILD_DIR)/share/enchant/myspell/en_AU.dic $(BUILD_DIR)/share/enchant/myspell/fr_FR.dic

#  Make enchant.
$(BUILD_DIR)/lib/libenchant.dll: $(ENCHANT_DIR)/Makefile
	cd $(ENCHANT_DIR) && make
	cp $(ENCHANT_DIR)/src/.libs/libenchant-1.dll $(BUILD_DIR)/lib/
	mkdir -p $(BUILD_DIR)/lib/enchant
	cp $(ENCHANT_DIR)/src/ispell/.libs/libenchant_ispell.dll $(BUILD_DIR)/lib/enchant/
	cp $(ENCHANT_DIR)/src/myspell/.libs/libenchant_myspell.dll $(BUILD_DIR)/lib/enchant/

$(ENCHANT_DIR)/Makefile: src/$(ENCHANT_DIR).tar.gz
	rm -rf $(ENCHANT_DIR)
	tar -xzvf src/$(ENCHANT_DIR).tar.gz
# FIXME are these patches still needed? It seems to work fine without them
#	patch $(ENCHANT_DIR)/src/enchant.c < patches/relocatable.patch
#	patch $(ENCHANT_DIR)/src/myspell/myspell_checker.cpp < patches/myspell_checker.patch
#	patch $(ENCHANT_DIR)/src/enchant-provider.h < patches/dllmain.patch
	cd $(ENCHANT_DIR) && ./configure CC="$(CC)" CXX="$(CXX)" ENCHANT_CFLAGS="$(ENCHANT_CFLAGS)" ENCHANT_LIBS="$(ENCHANT_LIBS)" $(ENCHANT_CONFIG_OPTS)


# Ability to extract MySpell dictionary files
$(BUILD_DIR)/share/enchant/myspell/%.dic: $(BUILD_DIR)/share/enchant/myspell/%.zip
	cd $(BUILD_DIR)/share/enchant/myspell && unzip -n $< '*.dic' '*.aff'


clean:
	rm -fr $(ENCHANT_DIR)

clobber: clean
	rm -f $(BUILD_DIR)/lib/libenchant*
	rm -rf $(BUILD_DIR)/lib/enchant
	rm -f $(BUILD_DIR)/share/enchant/myspell/*.dic
	rm -f $(BUILD_DIR)/share/enchant/myspell/*.aff
	rm -f $(BUILD_DIR)/share/enchant/myspell/*.txt

