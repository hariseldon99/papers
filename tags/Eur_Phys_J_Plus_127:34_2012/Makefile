PROP=./homogeneous_dynamics_simplify
PROP_JOURNAL=./homogeneous_dynamics_simplify_journal
LATEX=/usr/bin/latex
BIBTEX=/usr/bin/bibtex
PDFLATEX=/usr/bin/pdflatex
DVIPS=/usr/bin/dvips
PS2PDF=/usr/bin/ps2pdf

dvi:   
	echo ""
	echo " First run of LaTeX ..."
	echo ""
	$(LATEX) $(PROP)
	echo " Second run of LaTeX ..."
	echo ""
	$(LATEX) $(PROP)
	echo ""
	echo " Third run of LaTeX ..."
	echo ""
	$(LATEX) $(PROP)
	echo " Fourth run of LaTeX ..."
	echo ""
	$(LATEX) $(PROP)

# Make the postscript file from the .dvi file. The t option forces
# dvips to make the postscript file for letter (8.5 x 11) size paper.
#
pdf:
	echo ""
	echo " First run of LaTeX ..."
	echo ""
	$(LATEX) $(PROP)
	echo " Second run of LaTeX ..."
	echo ""
	$(LATEX) $(PROP)
	echo ""
	echo " Third run of LaTeX ..."
	echo ""
	$(LATEX) $(PROP)
	echo " Fourth run of LaTeX ..."
	$(LATEX) $(PROP)
	$(DVIPS) $(PROP).dvi
	$(PS2PDF) $(PROP).ps $(PROP).pdf

# Remove working files from last run.
#
clean:	
	rm -f $(PROP)*.log *.aux $(PROP)*.bbl $(PROP)*.blg $(PROP)*.dvi $(PROP)*.log $(PROP)*.ps $(PROP)*.out *~ *.backup

