.PHONY: all ref

all:
	@echo "# run all"
	@echo "DONE!"

ref: references.bib
	@echo "# run ref"
	cp $< temp.bib
	grep -v "file" temp.bib > $<
	rm -f temp.bib
	@echo "DONE!"
