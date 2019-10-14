# dependencies
# (*) nbnorm is the historical custom tool from flotpython
# (*) for nbpublish
#     pip install ipypublish 
# (*) with the sphinx engine (broken for us - unused)
#     pip install ipypublish[sphinx]
# (*) notebook concatenation
#     pip install nbmerge


NORMALIZE = ../../flotpython-tools/tools/nbnorm.py
NORMOPTS-THIERRY = --author "Thierry Parmentelat" --logo-path ../media/inria-25-alpha.png --rise --ipypublish
NORMOPTS-VALERIE = --author "Valérie Roy" --logo-path ../media/ensmp-25-alpha.png --rise --ipypublish
LICENCE_STRIP = ../../flotpython-gittutorial/tools/nbstriplicense.py


NB-THIERRY := $(shell git ls-files 1*.ipynb)
NB-VALERIE := $(shell git ls-files [23]*.ipynb)
NOTEBOOKS := $(NB-THIERRY) $(NB-VALERIE)

all:: norm 

norm:
	$(NORMALIZE) $(NORMOPTS-THIERRY) $(NB-THIERRY)
	$(NORMALIZE) $(NORMOPTS-VALERIE) $(NB-VALERIE)

#########################################################################
# publication
# 
# execution is done as part of sphinx-build
# there is only the need to mention the notebooks
# in index.rst
# 

#### sphinx

.PHONY: sphinx view-sphinx

sphinx: _build/html/index.html

_build/html/index.html: index.rst conf.py $(NOTEBOOKS) 
	sphinx-build -b html . _build/html

view-sphinx:
	open _build/html/index.html

### 
# markdown would be nice too, at least for creating a single bundled document
# unfortulately, terminal color sequences (like Esc-[-33m and similar) 
# end up unchanged and clobber the output, esp. for this course 
# so let's forget about that for now

clean:
	rm -rf _build
