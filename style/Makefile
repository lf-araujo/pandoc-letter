ifneq ("$(wildcard style/letterhead.md)","")
	LH := "style/letterhead.md"
endif

letter: $(LH) $(PDF) 
$(PDF): $(MD)
	pandoc -o $@ source/*.md $(TEXTEMPLATE) $(TEXFLAGS) 2>output/pdf.log
	if [[ "$OSTYPE" == "darwin" ]]; then open $@; else xdg-open $@;fi

$(LH): 
	pandoc -s -o style/letterhead.pdf $(LH) $(TEXFLAGS) 
