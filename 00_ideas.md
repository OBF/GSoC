---
layout: page
title: Project Ideas
permalink: /ideas/
---

# Google Summer of Code 2017 Project ideas

The details of each of our project ideas are listed below, including potential
mentors. Interested mentors and students should subscribe to the OBF/GSoC
mailing list and announce their interest.

See the [main OBF Google Summer of Code page](../) for more information about the GSoC
program and additional ways to get in touch with us.


#### Quick links

* Table of Contents
{:toc}

## Cross-project ideas

OBF is an umbrella organization which represents many different programming
languages used in bioinformatics. In addition to working with each of the
"Bio*" projects (listed below), this year we are also accepting a category of
"cross-project" ideas that cover multiple programming languages or projects.
These collaborative ideas are broadly defined and can be thought of as
"unfinished" — interested students should adapt the ideas to their own
strengths and goals, and are responsible for the quality of the final proposed
idea in their application.

**Feel free to propose your own entirely new idea.**

## GeneNetwork Genome Browser (biodalliance)

[GeneNetwork.org](http://gn2.genenetwork.org/) (GN) is a Web2.0
environment for genetic analysis in mouse, rat and human (QTL mapping
and GWAS). GN is used daily by scientists with over a thousand
publications citing it.

[Biodiallance.org](http://www.biodalliance.org/) is a state-of-the-art
Javascript genome browser. It is a fast, interactive, genome
visualization tool that's easy to embed in web pages and
applications. It supports integration of data from a wide variety of
sources, and can load data directly from popular genomics file formats
including bigWig, BAM, and VCF. Biodiallance has been adopted by some
major bioinformatics websites including, for example,
[UK10K](http://www.uk10k.org/dalliance.html).

#### Rationale

To improve user experience and improve biomedical discovery we are
improving advanced genome visualisation and embedding the
state-of-the-art [biodiallance genome
browser](http://www.biodalliance.org/) into GN with several new
*tracks* for visualizing mapped QTL, underlying genotypes and SNP
density.

![Biodalliance](https://sagebionetworks.jira.com/secure/attachment/24449/biodalliance%20widget%20output.png)

#### Approach

BioDiallance has good abstractions for tracks and fetching data. We
will add fetching data on-the-fly from GN backends through a
REST interface and/or cache locally. Also we will add interaction that
when a user
[clicks on a QTL](http://kbroman.org/qtlcharts/example/iplotScanone.html),
for example, the browser can display additional information and even
initiate some back-end processing.

We will use continuous
[open channels](http://www.phoenixframework.org/) between the browser
and the backend.

#### Languages and skill

Biodiallance is written in Javascript and the latest tracks support
[PureScript](http://www.purescript.org/). GeneNetwork is mostly python
and Javascript.  The GN REST interface is written in Elixir.

#### Code

* [Genenetwork.org](https://github.com/genenetwork)
* [Biodalliance](https://github.com/dasmoth/dalliance)

#### Difficulty
* <span class="medium">medium</span> mostly PureScript and Javascript, but python and elixir may come in handy

#### Mentors

[Pjotr Prins](https://github.com/pjotrp), [Danny Arends](https://github.com/dannyarends)  and
[Karl Broman](https://github.com/kbroman)

#### Contact

* IRC: `#genenetwork` on [Freenode](http://freenode.net/)
* [Mailing list GeneNetwork](http://listserv.uthsc.edu/mailman/listinfo/genenetwork-dev)
* [Mailing list Biodalliance](https://groups.google.com/forum/#!forum/biodalliance-dev)
* Direct: pjotr.public345 at thebird.nl


## antiSMASH

[antiSMASH](http://antismash.secondarymetabolites.org) is a tool to mine the
genomes of micro-organisms for biologically interesting gene clusters, so-called
secondary metabolites, to help find new antibiotics. It is a python-based  open
source tool that is developed at the Technical University of Denmark and Wageningen
University.

Project ideas around antiSMASH range from very close to applied biology to more
general software engineering projects.

### Improve gene cluster visualization (SVGene)

#### Rationale

antiSMASH generates a static HTML page report with prediction results for analysis runs.
This is the main UI used by the experimental biologists. To give an overview of the gene
cluster layout, antiSMASH uses the [SVGene](https://github.com/kblin/svgene) JavaScript library
to render gene cluster arrows as vector graphics. So far, this is a static SVG, with some
tooltip boxes added to provide the user with extra context:

![antiSMASH gene cluster](http://antismash.secondarymetabolites.org/static/images/panel1.jpg)

To further improve the user experience, zooming and panning should be implemented. Once
zoomed in, additional details can be displayed as well.

#### Approach

antiSMASH renders gene clusters using the [SVGene](https://github.com/kblin/svgene)
JavaScript library, which in turn is built on top of [D3.js](https://d3js.org/).
D3.js supports controls for pan and zoom that should be used for SVGene.
Gene cluster data for the HTML page is loaded from a JavaScript file included in the static
web page. Additional details should be displayed on a bigger zoom level if available, possibly
on separate tracks.

#### Languages and skill
SVGene is written in JavaScript and making heavy use of the [D3.js](https://d3js.org/)
library for drawing the SVG primitives.
Some Python knowledge might make it easier to extend antiSMASH's precalculated output,
but is not required, as mock inputs can be used for the project.

#### Code
* [antiSMASH on Bitbucket](https://bitbucket.org/antismash/antismash)
* [SVGene on github](https://github.com/kblin/svgene)

#### Difficulty
* <span class="easy">easy</span> with previous knowledge of D3.js
* <span class="medium">medium</span> otherwise

#### Mentors
[Kai Blin](https://github.com/kblin), Tilmann Weber


### SeqRecord access abstraction layer

#### Rationale
Internally, antiSMASH uses BioPython SeqRecord objects to handle the data. A lot
of the annotations are in custom feature entries or in free-text qualifiers of
"gene" or "CDS" features. Code for handling this access is duplicated in parts
of the code base. Additionally, directly using the SeqRecord object is a bit
fragile.

#### Approach
Code for accessing the antiSMASH-specific features/qualifiers should be hidden
behind an API layer that unifies the access. The new abstraction layer should
then be utilized to reduce the code duplication and fagility of acessing the
SeqRecord object special fields.

#### Languages and skill
antiSMASH is written in Python 2.7. Knowledge of unit testing in Python are a
plus. Biological knowledge is not required.

#### Code
* [Initial implementation of the abstraction
  library](https://github.com/kblin/python-secmet)
* [antiSMASH on Bitbucket](https://bitbucket.org/antismash/antismash)

#### Difficulty
<span class="easy">easy</span>

#### Mentors
[Kai Blin](https://github.com/kblin), Tilmann Weber

## OpenMS

[OpenMS](www.openms.de) is an open-source software C++ library for LC/MS data management and analyses. It offers an infrastructure for the rapid development of mass spectrometry related software. OpenMS is free software available under the three clause BSD license and runs under Windows, MacOSX and Linux. The source code is hosted publicly available on [GitHub](https://github.com/OpenMS/OpenMS/).

### Implement algorithms for the generation of high-resolution isotope patterns

#### Rationale

Mass spectrometry has become one of the bioanalytical tools of choice for many life scientists. Technological advancements in the last years have led to an increase in acquisition speed and resolution. Common tasks, like identifying and quantifying proteins and metabolites from biological or medical samples are regularly performed in different fields of research, industry, and clinical diagnostics.

Modern mass spectrometers are becoming more and more capable of resolving not only the mass of a molecule but also of its naturally occurring variants with different isotopic composition. Simply speaking, if the "isotopic fine structure" is known, the exact chemical formula can be derived and be used to resolve ambiguities in the identification of molecules. 

#### Approach

OpenMS currently includes a theoretical isotope pattern generator that calculates a coarse version of the isotopic structure.

Several papers have been published that describe implementations of a high-resolution isotope pattern algorithm, e.g.:
[MIDAS](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3880471/) and 
[Mercury5](https://www.ncbi.nlm.nih.gov/pubmed/21619291)

for which reference implementations are provided by the authors. They could be potentially interesting algorithms that can be validated against a reference implementation.

OpenMS tool developers and users alike would benefit from well-tested, native implementations using the OpenMS library. In the future, this implementation could be used by others to build novel tools or improve existing ones. 

#### Languages and skills

* Intermediate knowledge of C++ and its STL. Knowledge of Boost's Math Library might be of use.
* Depending on the implemented algorithm, intermediate knowledge of polynomial algebra and mathematical convolutions.
* Basic knowledge on atom masses and isotopes (can be acquired in the first days).
* Basic knowledge on mass spectrometry (can be acquired in the first days).

#### Code

Expected outcome:
The existing implementation for low-resolution data in OpenMS ([IsotopeDistribution]( https://github.com/OpenMS/OpenMS/blob/e2eda7b3ef61dd22dd8f704d7b26db7635ba33e9/src/openms/source/CHEMISTRY/IsotopeDistribution.cpp)) should be extended by at least one algorithm for high-resolution data.
We suggest the MIDAS and Mercury5 algorithm but are open for suggestions.
Pseudocode and reference implementations can be provided and found in the publications.

#### Difficulty
<span class="easy">medium</span>.

#### Mentors
[Timo Sachsenberg](https://github.com/timosachsenberg), [Julianus Pfeuffer](https://github.com/jpfeuffer)
