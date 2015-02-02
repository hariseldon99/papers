WORK=${PWD}
TAR=/bin/tar
USE_PDFLATEX=true
VIEWPDF=okular

FILENAME=isingrand
MAIN_FILENAME=DMF-Random-V4
SUPPL_FILENAME=DMF-Random_suppl
NAME=${MAIN_FILENAME} ${SUPPL_FILENAME}
BIBFILE=bib_freezing
NO_HYPERTEX=00README.XXX

EXTRA_DIST+=${BIBFILE}.bib *.gmk Makefile

FIGS_HIRES_MAIN=fig1_hires.eps fig2_hires.eps fig3_hires.eps
FIGS_HIRES_SUPPL=supp_fig1_hires.eps supp_fig2_hires.eps supp_fig3_hires.eps
FIGS_LOWRES_MAIN=fig1_lowres.eps fig2_lowres.eps fig3_lowres.eps
FIGS_LOWRES_MAIN_PDF=fig1_lowres.pdf fig2_lowres.pdf fig3_lowres.pdf
FIGS_LOWRES_SUPPL=supp_fig1_lowres.eps supp_fig2_lowres.eps supp_fig3_lowres.eps

CLEAN_FILES+=*.backup *converted-to.pdf ${MAIN_FILENAME}.pdf ${SUPPL_FILENAME}.pdf *Notes.bib *.aux *.log *.out ${SUPPL_FILENAME}.bbl

include latex.gmk

tarball_full:
	${TAR} -cvf ${FILENAME}_full.tar *.tex $(EXTRA_DIST) $(FIGS_HIRES_MAIN) $(FIGS_LOWRES_MAIN) $(FIGS_HIRES_SUPPL) $(FIGS_LOWRES_SUPPL)
	gzip ${FILENAME}_full.tar

tarball:
	${TAR} -cvf ${FILENAME}.tar *.tex $(EXTRA_DIST) $(FIGS_HIRES_MAIN) $(FIGS_HIRES_SUPPL)
	gzip ${FILENAME}.tar

arxiv:
	$(foreach file,$(FIGS_LOWRES_MAIN),epstopdf $(file);)
	#Build the supplementary PDF the old way to compress it
	echo '%&latex' | cat - ${SUPPL_FILENAME}.tex | tee ${SUPPL_FILENAME}.tex
	latex ${SUPPL_FILENAME}
	bibtex ${SUPPL_FILENAME}
	latex ${SUPPL_FILENAME}
	latex ${SUPPL_FILENAME}
	dvips ${SUPPL_FILENAME}
	ps2pdf ${SUPPL_FILENAME}.ps
	pdftk ${SUPPL_FILENAME}.pdf output ${SUPPL_FILENAME}_compressed.pdf compress
	mv ${SUPPL_FILENAME}_compressed.pdf ${SUPPL_FILENAME}.pdf
	${TAR} -cvf ${FILENAME}_arxiv.tar $(NO_HYPERTEX) ${MAIN_FILENAME}.tex ${MAIN_FILENAME}.bbl $(FIGS_LOWRES_MAIN_PDF) ${SUPPL_FILENAME}.pdf
	gzip ${FILENAME}_arxiv.tar
	#Revert the supplementary file back to pristine condition
	sed -i '1d' ${SUPPL_FILENAME}.tex
