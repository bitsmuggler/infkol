PDFPARAMS=-s -t latex --pdf-engine=xelatex -V documentclass=scrartcl -V papersize=a4 -V lang=en
FONTPARAMS=-V mainfont='DejaVu Serif' -V sansfont='DejaVu Sans' -V monofont='DejaVu Sans Mono' -V fontsize=11pt
DATE=-V date="`date +'%Y-%m-%d'`"

all: 1-managerial-skills/summary-q-a_bucher-christensen.pdf 2-kafka/summary-questions_bucher.pdf

1-managerial-skills/summary-q-a_bucher-christensen.pdf: 1-managerial-skills/*.md
	# pandoc $(PDFPARAMS) $(FONTPARAMS) $(DATE) $^ -o $@
	pandoc $^ -t ms -o $@

2-kafka/summary-questions_bucher.pdf: 2-kafka/*.md
	pandoc $^ -t ms -o $@

clean:
	rm -f 1-managerial-skills/summary-q-a_bucher-christensen.pdf
	rm -f 2-kafka/summary-questions_bucher.pdf
