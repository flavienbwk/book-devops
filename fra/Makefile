# Build configuration

BUILD = build
MAKEFILE = Makefile
OUTPUT_FILENAME = book
METADATA = metadata.yml
ifneq ($(wildcard ./PREFACE.md),)
    CHAPTERS = ./PREFACE.md ./README.md
else
    CHAPTERS = ./README.md
endif
TOC = --toc --toc-depth 2
METADATA_ARGS = --metadata-file $(METADATA)
IMAGES = $(shell find images -type f)
TEMPLATES = $(shell find templates/ -type f)
ifneq ($(wildcard ./images/cover_a5_source_preface.png),)
	COVER_IMAGE = images/cover_a5_source_preface.png
else
	COVER_IMAGE = images/cover_a5_source.png
endif
MATH_FORMULAS = --webtex

# Chapters content
CONTENT = awk 'FNR==1 && NR!=1 {print "\n\n"}{print}' $(CHAPTERS)
CONTENT_FILTERS = tee # Use this to add sed filters or other piped commands

# Debugging

# DEBUG_ARGS = --verbose

# Pandoc filtes - uncomment the following variable to enable cross references filter. For more
# information, check the "Cross references" section on the README.md file.

# FILTER_ARGS = --filter pandoc-crossref

# Combined arguments

ARGS = $(TOC) $(MATH_FORMULAS) $(METADATA_ARGS) $(FILTER_ARGS) $(DEBUG_ARGS)
	
PANDOC_COMMAND = pandoc

# Per-format options

DOCX_ARGS = --standalone --reference-doc templates/docx.docx
EPUB_ARGS = --template templates/epub.html --epub-cover-image $(COVER_IMAGE)
HTML_ARGS = --template templates/html.html --standalone --to html5
PDF_ARGS = --template templates/pdf.latex --pdf-engine xelatex

# Per-format file dependencies

BASE_DEPENDENCIES = $(MAKEFILE) $(CHAPTERS) $(METADATA) $(IMAGES) $(TEMPLATES)
DOCX_DEPENDENCIES = $(BASE_DEPENDENCIES)
EPUB_DEPENDENCIES = $(BASE_DEPENDENCIES)
HTML_DEPENDENCIES = $(BASE_DEPENDENCIES)
PDF_DEPENDENCIES = $(BASE_DEPENDENCIES)

# Detected Operating System

OS = $(shell sh -c 'uname -s 2>/dev/null || echo Unknown')

# OS specific commands

ifeq ($(OS),Darwin) # Mac OS X
	COPY_CMD = cp -P
else # Linux
	COPY_CMD = rsync -vrP --exclude "*.psd" --exclude "*.pdf" --exclude "*.bkp" --exclude "*.dtmp" --exclude "*.drawio" --ignore-missing-args
endif

MKDIR_CMD = mkdir -p
RMDIR_CMD = rm -r
ECHO_BUILDING = @echo "building $@..."
ECHO_BUILT = @echo "$@ was built\n"

.PHONY: all book clean epub html pdf docx

all:	book

book:	epub html pdf docx

clean:
	$(RMDIR_CMD) $(BUILD)

epub:	$(BUILD)/epub/$(OUTPUT_FILENAME).epub

html:	$(BUILD)/html/index.html

pdf:	$(BUILD)/pdf/$(OUTPUT_FILENAME).pdf

docx:	$(BUILD)/docx/$(OUTPUT_FILENAME).docx

$(BUILD)/epub/$(OUTPUT_FILENAME).epub:	$(EPUB_DEPENDENCIES)
	$(ECHO_BUILDING)
	$(MKDIR_CMD) $(BUILD)/epub
	$(CONTENT) | $(CONTENT_FILTERS) | $(PANDOC_COMMAND) $(ARGS) $(EPUB_ARGS) -o $@
	$(ECHO_BUILT)

$(BUILD)/html/index.html:	$(HTML_DEPENDENCIES)
	$(ECHO_BUILDING)
	$(MKDIR_CMD) $(BUILD)/html/images
	$(CONTENT) | $(CONTENT_FILTERS) | $(PANDOC_COMMAND) $(ARGS) $(HTML_ARGS) -o $@
	$(COPY_CMD) $(IMAGES) $(BUILD)/html/images/
	$(ECHO_BUILT)

$(BUILD)/pdf/$(OUTPUT_FILENAME).pdf:	$(PDF_DEPENDENCIES)
	$(ECHO_BUILDING)
	$(MKDIR_CMD) $(BUILD)/pdf
	$(CONTENT) | $(CONTENT_FILTERS) | $(PANDOC_COMMAND) $(ARGS) $(PDF_ARGS) -o $@
	convert ./images/fourthcover_a5_source.png ./images/fourthcover_a5_source.pdf;
	convert ./images/cover_a5_source.png ./images/cover_a5_source.pdf;
	if [ -f ./images/cover_a5_source_preface.png ]; then \
		convert ./images/cover_a5_source_preface.png ./images/cover_a5_source_preface.pdf; \
		pdftk ./images/cover_a5_source_preface.pdf $(BUILD)/pdf/$(OUTPUT_FILENAME).pdf ./images/fourthcover_a5_source.pdf cat output $(BUILD)/pdf/book_covered_preface.pdf; \
	fi;
	pdftk ./images/cover_a5_source.pdf $(BUILD)/pdf/$(OUTPUT_FILENAME).pdf ./images/fourthcover_a5_source.pdf cat output $(BUILD)/pdf/book_covered.pdf;
	$(ECHO_BUILT)

$(BUILD)/docx/$(OUTPUT_FILENAME).docx:	$(DOCX_DEPENDENCIES)
	$(ECHO_BUILDING)
	$(MKDIR_CMD) $(BUILD)/docx
	$(CONTENT) | $(CONTENT_FILTERS) | $(PANDOC_COMMAND) $(ARGS) $(DOCX_ARGS) -o $@
	$(ECHO_BUILT)
