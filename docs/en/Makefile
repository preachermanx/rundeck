include ../Makefile.inc

#APIVERS=1
APIVERS=$(shell cat api/version.info)

DIRS = manpages
CSS = style.css
DIST = dist
DATE = $(shell date "+%m-%d-%Y% %H:%M")
ifndef VERSION
VERSION=$(shell grep version.number= ../../version.properties | cut -d= -f 2)
endif

EDAM=groovy edam.groovy

.PHONY: man html clean oldlinks

all : man html resources

man : 
	mkdir -p $(DIST)
	$(MAKE) VERSION=$(VERSION) -C manpages/man1
	$(MAKE) VERSION=$(VERSION) -C manpages/man5

html: oldlinks
	mkdir -p $(DIST)/html
	$(EDAM) -o $(DIST)/html -r -O 'recurseDirPatternIgnore=(dist|figures|oldlinks|temp)' -V "VERSION=$(VERSION)" -V "APIVERS=$(APIVERS)"

oldlinks: oldlinks/*.md
	mkdir -p $(DIST)/html
	$(EDAM) -o $(DIST)/html -d oldlinks -t templates


resources :  $(CSS) ../figures/*.png
	mkdir -p $(DIST)/html/figures
	- cp ../figures/*.png $(DIST)/html/figures
	cp $(CSS) $(DIST)/html/

clean :
	rm -fr $(DIST)
	$(MAKE) -C manpages/man1 clean
	$(MAKE) -C manpages/man5 clean
