# Letter Template for Pandoc

If you are used to `mighty_make`, just do:

```bash
make fetch THEME="https://github.com/lf-araujo/pandoc-letter"
```
---

It's been a while since the creation of [Mighty_Make](https://lf-araujo.github.io/2017/04/08/mightymake.html) and I have learned more about creating a builder with [GNU's Make](https://www.gnu.org/software/make/). The last  published  example on quickly creating a document with pandoc was a [letter pandoc template](https://lf-araujo.github.io/2017/04/08/zletter.html). Here it will be revisited, as the template received alterations over the last year. As usual the division between style, content, and tool will be followed and this small text will mainly discuss the style.

For the production of the pandoc generated documents a strikingly effective workflow uses [Sublime Text 3](https://lf-araujo.github.io/2016/11/07/mdworkflow.html). This alone should take care of most text edition needs. 

The styling of letters in LaTeX can be done with multiple classes. However, these are usually an overkill for such a simple task. The template previously published among these notes was inspired by Mattia Tezzele’s [work](http://mrzool.cc/writing/typesetting-automation/) and the following will still be.

The following template is published in the same github repository as before. It consists of the latest version of Mighty_Make where the user will only need to change two files. The first file  is  the  `source/letter.md` and the second is the `style/letterhead.md`. The latter should only be edited/used in case the user represents a company or has a small company for which she wants to create a letterhead.

In the yaml header a `letterhead: true` options is available. If present it will create a letterhead, similar to Mattia Tezzele’s letter with letterhead and if absent it will create a letter with a simpler but elegant titling (more like a header).

To follow the example one needs to have `git`, `pandoc`, `pandoc-citeproc`, and `pandoc-crossref` installed in the system. It starts by installing the package:

```bash
git clone https://github.com/lf-araujo/pandoc-letter.git
```

Edit the aforementioned files and `cd` into the base directory and run `make`. The tool now runs in Windows (it is probably quicker to install it in the Linux Subsystem for Windows), Mac and Linux. That is it, the `make` command will open the document produced at the `output` directory once it is finished.
