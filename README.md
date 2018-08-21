# Letter Template for Pandoc

If you are used to `mighty_make`, just do:

```bash
make fetch THEME="https://github.com/lf-araujo/pandoc-letter"
```
---

This project is an improvement of Mattia Tezzele's [work](http://mrzool.cc/writing/typesetting-automation/). It is also an example for the use of the Mighty Make tool I have shown in the previous [post](https://lf-araujo.github.io/lf-araujo.github.io/2017/04/08/mightymake.html). I have been using his approach for more than a year now, it is quite useful to automate the creation of letters. In his version, however, there is no easy way of creating a letterhead. In what follows, you can find the automation of most of the steps, including the letterhead.

This is how it looks:

![](  /images/Captura de tela de 2017-12-26 20-18-27.png )


If you already understand the process or do not want to read a step-by-step explanation, you can simply clone my project at github and edit both the `/style/letterhead.md` and the `/source/letter.md` files. The command for cloning is:

```bash
git clone https://github.com/lf-araujo/pandoc-letter.git
```

Otherwise, you can follow instructions and understand what is being done behind the curtains. First, download mighty-make:

```bash
wget http://bit.ly/2oOlPXY -O Makefile
```

## Update

**The following is not necessary anymore with mighty_make reaching v1. However, I will keep the code here for easy inspection of what I do inside the Makefile.**

Edit the makefile with: 

```make
pdf: letterhead
	pandoc "$(INPUTDIR)/"*.md \
	-o "$(OUTPUTDIR)/$(NAME).pdf" \
	$(TEXTEMPLATE) \
	$(TEXFLAGS)
	xdg-open "$(OUTPUTDIR)/$(NAME).pdf"

letterhead:
	pandoc "$(STYLEDIR)/letterhead"*.md \
	-o "$(STYLEDIR)/letterhead.pdf" \
```

This previous code is adding a dependency to the pdf creation, where pandoc will run once to generate a letterhead and save it to the /style directory. But for it to work, we need a letterhead.md placed at the same /style directory:

## After mighty_make v1

One can simply import the `letter` theme with:

```bash
make fetch THEME="https://github.com/lf-araujo/pandoc-letter"
```

## Use

If you followed the instructions above, just go on and edit the source file inside `/source` and build the document (Ctrl+B if you use Sublime Text 3 and follows my [workflow](https://lf-araujo.github.io/2016/11/07/mdworkflow.html)). In the following paragraph I explain the inner parts of the package, this information should only be interesting to the curious, it is also an example of how modular mighty_make is.



```markdown
---
fontsize: 7pt
lang: en
geometry: left=22mm, right=10mm, top=50mm
mainfont: "Minion Pro"
mainfontoptions:
    - Mapping=tex-text
    - Numbers=OldStyle
    - Letters=SmallCaps
monofont: 'Fira Mono'
header-includes:
	- \usepackage[usenames,dvipsnames]{color}
	- \usepackage{xcolor}
---

\color{blue!30!black}
\pagenumbering{gobble}
**F. Nietzsche**

\vspace{10mm} 

Some department at the Uni

The Building

The University
 
\vspace{5mm} 

Street

Address 1

Adddress 2

Naumbur
 
\vspace{5mm} 

\texttt{email@protonmail.com}

```

One can change the color for the letterhead by changing the line `\color{blue!30!black}`.

The second step involves creating a custom template at the /style directory. This template will organize both the letterhead and the other typographic elements. The template can be created with `touch template.tex` and with `subl3 template.tex` add the contents from the [file](https://github.com/lf-araujo/pandoc-letter/blob/master/style/template.tex).


Now we are ready to write the letter itself, cd into the /source directory and create the letter with `touch letter.md` and with `subl3 letter.md` add the following (edit to your needs):

```markdown
---
subject: This is the subject
author: F. Nietzsche
city: Heidelberg
from:
- Heidelberg
linestretch: 1.1
# Settings
mainfont: "Minion Pro"
mainfontoptions:
- Mapping=tex-text
- Scale=1
altfont: Fira Sans
monofont: Fira Mono
lang: en
fontsize: 12pt
geometry: a4paper, left=82mm, right=22mm, top=50mm, bottom=25mm
letterhead: true
# customdate: YYYY-MM-DD
---

Hello,


This is a long letter to my friend




Kind Regards,
```

## Not into fancy letterheads?

Easy enough, just change two lines from the yaml block (the block separated by ---), to:

```yaml
# geometry: a4paper, left=82mm, right=22mm, top=50mm, bottom=25mm
letterhead: false
```

What we did there was to disable the letterhead and let the text flow freely across the page.

This is how it will look like:

![](  /images/Captura de tela de 2017-12-28 08-15-02.png )

## Conclusion

Finally, note that the template allows adding a signature in PDF format. In order to achieve that you need to create your own following the instructions from [here](http://tex.stackexchange.com/questions/32911/adding-a-signature-on-an-online-job-application/32940#32940), which Mattia suggested in his [page](http://mrzool.cc/writing/typesetting-automation/) as well. The resulting file is the best typeset letter one can achieve using markdown. Enjoy.
