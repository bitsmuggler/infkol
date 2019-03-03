PDFPARAMS=-s -t latex --pdf-engine=xelatex -V documentclass=scrartcl -V papersize=a4 -V lang=en
FONTPARAMS=-V mainfont='DejaVu Serif' -V sansfont='DejaVu Sans' -V monofont='DejaVu Sans Mono' -V fontsize=11pt
DATE=-V date="`date +'%Y-%m-%d'`"

all: 1-managerial-skills/summary-questions_bucher-christensen.pdf

1-managerial-skills/summary-questions_bucher-christensen.pdf: 1-managerial-skills/*.md
	pandoc $(PDFPARAMS) $(FONTPARAMS) $(DATE) $^ -o $@

clean:
	rm -f 1-managerial-skills/summary-questions_bucher-christensen.pdf
