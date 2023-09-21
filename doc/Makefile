# Makefile for LaTeX document with BibTeX

# Replace 'main' with the name of your main .tex file (without the .tex extension)
MAIN = main
OUTPUT = output/$(MAIN).pdf

all: pdf

clean:
	rm -rf *.aux *.bbl *.blg *.log *.out *.pdf *.toc *.dvi *.lof *.lot *.fdb_latexmk *.fls *.synctex.gz

pdf:
	pdflatex $(MAIN)
	bibtex $(MAIN)
	pdflatex $(MAIN)
	pdflatex $(MAIN)
	mv $(MAIN).pdf $(OUTPUT)
	make clean

.PHONY: all clean pdf