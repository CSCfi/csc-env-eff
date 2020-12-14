LECTURES=00_study_tips.md \
02_logging_in.md \
10_speed_up_jobs.md \
example.md
# remove example and add other chapters here

TITLE=Title.pdf

PRESS=csc-env-press.pdf
HANDOUT=csc-env--handout.pdf

PANDOC=$(HOME)/bin/pandoc.sif

HTMLS:=$(patsubst %.md,%.html,$(LECTURES))
PDFS:=$(patsubst %.md,%.pdf,$(LECTURES))

all: $(PDFS)
	echo -c $(TITLE) -o $(PRESS) -h $(HANDOUT) -- $(PDFS)

%.html:%.md
	$(PANDOC) -s $<

%.pdf:%.html
	echo $<

.PHONY: clean

clean:
	-/bin/rm -f $(HTMLS) $(PDFS) $(PRESS) $(HANDOUT) *~

.PRECIOUS: %.html
