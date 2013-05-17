# LaTeX support files for peg-multimarkdown

## Modifications for the Use with Scrivener

Basically, this is the project as described below. I just changed some things for using the package with [Scrivener](http://www.literatureandlatte.com/scrivener.php).
Projects that I write with Scrivener are exported as LaTeX with the classes *Article* or *Memoir* and then finalized with [texmaker](http://www.xm1math.net/texmaker/).

### BibTeX

If you want to link a database with references (.bib) to the tex-file, you can enter this in the Meta-Data settings in the Compile dialogue:

    BibTeX: name-of-your-refs

### BibLaTeX

As you can see in `mmd-memoir-packages.tex` I changed the reference management to BibLaTeX

    \usepackage[citestyle=authoryear,style=authoryear,sorting=nty]{biblatex}

This means that you need to change some lines of code in `mmd-memoir-footer.tex` and print out the bibliography with

    \printbibliography

As Scrivener will produce a line of TeX code from this that looks like the following:

    \def\bibliocommand{\bibliography{refs}}

you will manually have to change this to

    \bibliography{refs}

and put the refs-file relative to the tex-file.

This could work! :-)

Thanks to the Markdown folks for the amazing opportunities around this way of writing!

## Introduction #

[peg-multimarkdown] is  a program to  convert plain  text into HTML  or LaTeX.
This project includes  some default template files that can  be used to create
certain types of documents using LaTeX.

You are not limited  to using these classes or templates.  You can create your
own template files, or just embed  your LaTeX commands within comments in your
MultiMarkdown document itself. If you find yourself creating similar documents
over and over again,  however, you may be better off  creating a few templates
you can simply call with the `LaTeX Input` metadata fields in MultiMarkdown.

These files were  designed to handle some  of the common metadata  fields in a
consistent way, an to implement some  defaults that *should* prevent errors if
you leave out important metadata (substituting `Title`, `Author`, etc).

[peg-multimarkdown]: https://github.com/fletcher/peg-multimarkdown


## Installation #

These files need to go in your `texmf` folder, wherever that may be.

With MacTeX on Mac OS X:

	~/Library/texmf/tex/latex/mmd

On most *nix accounts, you can use:

	~/texmf/tex/latex/mmd

I don't  remember off the top  of my head  where your texmf folder  belongs in
Windows.


## Default Metadata Types #

Several MultiMarkdown  metadata keys are used  in these files, and  are fairly
self-explanatory:

* Title				--- Specify the title of the document

* Author			--- Specify the author of the document

* Date				--- Specify a date

* Base Header Level --- Specify the maximum organizational level for the
  document (e.g. part, chapter, section, subsection). You need to choose a
  value for this that fits with the way you organized your document.

Metadata is  used in order,  so the order and  placement of the  `LaTeX Input`
metadata fields is important.


## Article #

To create  a document using the  memoir article class, you  need the following
basic metadata:


	latex input:		mmd-article-header
	Title:				Whatever Title You Like 
	Base Header Level:	2  
	LaTeX Mode:			memoir  
	latex input:		mmd-article-begin-doc
	latex footer:		mmd-memoir-footer


## Beamer #

To create a pdf slideshow presentation using beamer:

	latex input:		mmd-beamer-header  
	Title:				Your Title  
	Subtitle:			Some optional subtitle 
	Author:				Your Name  
	Affiliation:		Your institution, web site, whatever
	base header level:	3
	LaTeX Mode:			beamer  
	Theme:				keynote-gradient  
	latex input:		mmd-beamer-begin-doc  
	latex footer:		mmd-beamer-footer  

There are several beamer themes included that are derived from various keynote
themes  --- keynote-gradient,  keynote-vintage,  keynote-portfolio. I  tweaked
these themes to  work with MultiMarkdown, but they were  originally created by
others (see the source files for details).

The header levels are set so that `h1` is a part, `h2` is a section, `h3` is a
slide, and `h4`  is used to designate  text that will print in  a handout, but
not in the actual slideshow.


## Letterhead #

To create a letter on customized letterhead using MultiMarkdown:

	latex input:		mmd-letterhead-header  
	Title:				Test Letter  
	Author:				John Doe  
	email:				fletcher@example.net  
	address:			123 Main St.  
						Some City, ST  12345  
	recipient:			Some Person  
	Recipient Address:	321 Main St  
						Some City, ST  54321  
	phone:				(555) 555-5555  
	Date:				December 15, 2007  
	latex xslt:			custom-letterhead.xslt  
	black and white:	true  
	base header level:	2  
	latex mode:			memoir  
	latex footer:		mmd-letterhead-footer  
	latex input:		mmd-letterhead-begin-doc  

If you want to create an envelope using the same document, simply change the
last line of the metadata:

	latex input:		mmd-envelope-begin-doc


## Memoir #

To create a "book" using memoir:

	latex input:		mmd-memoir-header
	Title:				Your Title
	Base Header Level:	2
	LaTeX Mode:			memoir  
	latex input:		mmd-memoir-begin-doc
	latex footer:		mmd-memoir-footer

Header levels  are: `h1`  part, `h2` chapter,  `h3` section,  `h4` subsection,
`h5` subsubsection, and `h6` paragraph.
