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
"Bio\*" projects (listed below), this year we are also accepting a category of
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

[OpenMS](www.openms.de) is an open-source software C++ library for LC/MS data
management and analyses. It offers an infrastructure for the rapid development
of mass spectrometry related software. OpenMS is free software available under
the three clause BSD license and runs under Windows, MacOSX and Linux. The
source code is hosted publicly available
on [GitHub](https://github.com/OpenMS/OpenMS/).

### Implement algorithms for the generation of high-resolution isotope patterns

#### Rationale

Mass spectrometry has become one of the bioanalytical tools of choice for many
life scientists. Technological advancements in the last years have led to an
increase in acquisition speed and resolution. Common tasks, like identifying and
quantifying proteins and metabolites from biological or medical samples are
regularly performed in different fields of research, industry, and clinical
diagnostics.

Modern mass spectrometers are becoming more and more capable of resolving not
only the mass of a molecule but also of its naturally occurring variants with
different isotopic composition. Simply speaking, if the "isotopic fine
structure" is known, the exact chemical formula can be derived and be used to
resolve ambiguities in the identification of molecules.

#### Approach

OpenMS currently includes a theoretical isotope pattern generator that calculates a coarse version of the isotopic structure.

Several papers have been published that describe implementations of a high-resolution isotope pattern algorithm, e.g.:
[MIDAS](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3880471/) and 
[Mercury5](https://www.ncbi.nlm.nih.gov/pubmed/21619291)

for which reference implementations are provided by the authors. They could be
potentially interesting algorithms that can be validated against a reference
implementation.

OpenMS tool developers and users alike would benefit from well-tested, native
implementations using the OpenMS library. In the future, this implementation
could be used by others to build novel tools or improve existing ones.

#### Languages and skills

* Intermediate knowledge of C++ and its STL. Knowledge of Boost's Math Library might be of use.
* Depending on the implemented algorithm, intermediate knowledge of polynomial algebra and mathematical convolutions.
* Basic knowledge on atom masses and isotopes (can be acquired in the first days).
* Basic knowledge on mass spectrometry (can be acquired in the first days).

#### Code

Expected outcome:

The existing implementation for low-resolution data in OpenMS
([IsotopeDistribution]( https://github.com/OpenMS/OpenMS/blob/e2eda7b3ef61dd22dd8f704d7b26db7635ba33e9/src/openms/source/CHEMISTRY/IsotopeDistribution.cpp))
should be extended by at least one algorithm for high-resolution data.

We suggest the MIDAS and Mercury5 algorithm but are open for suggestions.
Pseudocode and reference implementations can be provided and found in the publications.

#### Difficulty
<span class="medium">medium</span>.

#### Mentors
[Timo Sachsenberg](https://github.com/timosachsenberg), [Julianus Pfeuffer](https://github.com/jpfeuffer)


## Common Workflow Language

The Common Workflow Language standards enable bioinformaticians and other
researchers to describe their data analysis workflows in a portable,
interopable, and executable manner without being dependent on a particular
workflow system.

![CWL viewer](https://pbs.twimg.com/media/C3rzBPbWEAAX2rt.png)

(image from
https://view.commonwl.org/workflows/github.com/common-workflow-language/workflows/tree/master/workflows/lobSTR
)

### CWL reference implementation (cwltool)

[cwltool](https://github.com/common-workflow-language/cwltool) is the reference
implementation of the [Common Workflow Language](http://www.commonwl.org/).
cwltool's main purpose is demonstrate the majority of the features of CWL by
executing data analysis tools and workflows described in CWL v1.0 documents.

It is intended to be feature complete and provide comprehensive validation of
CWL files as well as provide other tools related to working with CWL.

#### Rationale

The goal of the project is to enhance cross platform compatibility and
usability of cwltool, specifically by migrating to Py2+3 and adding Microsoft
Windows support

* Python 3 support for [schema-salad](http://www.commonwl.org/v1.0/SchemaSalad.html)
  (rules for preprocessing, structural validation, and link checking for CWL
  documents) and cwltool overall
* Windows support for cwltool, configuring continuous integration to keep it
  from breaking
* Resolving some of the [Github issues](https://github.com/common-workflow-language/cwltool/issues)
  on the way

#### Approach

cwltool uses continious [conformance testing](https://ci.commonwl.org/job/cwltool-conformance/)
to comply with the latest specification. 

#### Languages and skill

cwltool is written and tested for Python 2.7. Python 3 experience, familiarity
with unit and continious testing is desired. No background in data intensive
science is required.

#### Code

* [cwltool](https://github.com/common-workflow-language/cwltool)

#### Difficulty
* <span class="medium">medium</span>

#### Mentors

[Michael R. Crusoe](https://github.com/mr-c), [Anton Khodak](https://github.com/anton-khodak)

#### Contact

* [Gitter](https://gitter.im/common-workflow-language/common-workflow-language)
* [Mailing list](https://groups.google.com/forum/#!forum/common-workflow-language)
* [Question & Answer](https://www.biostars.org/t/cwl)

### Add IO streaming to CWL reference implementation

You can mark parts of a data analysis workflow as supporting streaming IO when
using the Common Workflow Language via the [`streamable: true` directive
](http://www.commonwl.org/v1.0/CommandLineTool.html#CommandInputParameter)

#### Rationale

However,  [cwltool](https://github.com/common-workflow-language/cwltool) (the reference
implementation of the [Common Workflow Language](http://www.commonwl.org/))
does not implement any streaming IO optimzation and ignores the `streamable`
flag.


In order to add streaming support `cwltool` will also need to be able to
execute steps simultaneously.

#### Approach
One of the goals of the reference implementation is to have a simple code base
to enhance learning and simplify maintenance.

This project will require studying multiple methods of enabling co-execution of
steps (and enabling streaming IO via unix named FIFOs ("pipes")) and choosing
the method that produces the most maintable code. Preferably external libraries
that are well maintained and well documented are used to keep code growth to a
minimum.

cwltool uses continious [conformance testing](https://ci.commonwl.org/job/cwltool-conformance/)
to comply with the latest specification. 

#### Languages and skill

cwltool is written and tested for Python 2.7. Python 3 experience, familiarity
with unit and continious testing is desired. No background in data intensive
science is required.

#### Code

* [cwltool](https://github.com/common-workflow-language/cwltool)

#### Difficulty
* <span class="medium">medium</span>

#### Mentors

[Michael R. Crusoe](https://github.com/mr-c)

#### Contact

* [Gitter](https://gitter.im/common-workflow-language/common-workflow-language)
* [Mailing list](https://groups.google.com/forum/#!forum/common-workflow-language)
* [Question & Answer](https://www.biostars.org/t/cwl)


## ETE TOOLKIT

The ETE toolkit is a Python software intended for the integrative
reconstruction, analysis and visualization
of [phylogenetic trees](https://en.wikipedia.org/wiki/Phylogenetic_tree). ETE is
widely used in the computational biology field, particularly for large phylogenomic studies (>270
citations, >3000 ETE 3.0 downloads).

* [Website](http://etetoolkit.org)
* [Support Mailing list](https://groups.google.com/forum/#!forum/etetoolkit)
* [Documentation](http://etetoolkit.org/docs/latest/tutorial/index.html) and [cookbook](http://etetoolkit.org/cookbook/)
* [Github](https://github.com/etetoolkit/ete)
* [ETE 3 paper](https://academic.oup.com/mbe/article/33/6/1635/2579822/ETE-3-Reconstruction-Analysis-and-Visualization-of?searchresult=1) 

### GSoC Contact
If interested in any of the following project ideas, or you want to propose a new one,
please contact us early, preferably at **ete-gsoc-mentors@googlegroups.com**

### 1. Developing a novel format for phylogenomic data**

#### Rationale

Phylogenetic trees are usually encoded using the so
called [Newick format](https://en.wikipedia.org/wiki/Newick_format). While
convenient, this format has limitations to store metadata associated to the
different nodes in a tree. Some alternative formats exist (NeXML, PhyloXML,
Nexus) which are already supported by the ETE toolkit. However, none of those
formats is optimal to i) encode ETE graphical properties associated to nodes ii)
store large trees or huge collections of trees iii) access metadata from large
datasets in an indexed way.

In addition, a community of developers specialized in tree visualization
software is brainstorming about possible ways to make the process of composing
and sharing figures more portable and transparent. It is expected that this
project keeps in sync with the
expected
[outcome of such meetings](https://github.com/OpenTreeOfLife/treeviz-workshop-2017/wiki#expected-outcomes) and
provide support for the conventions and tree annotation vocabulary agreed.

#### Goals

1. Develop a data format capable of storing trees, metadata and graphical
   features associated to nodes. The following features are ambitioned: Tree
   structure and node metadata indexing, data compression, possibility of having
   multiple trees in a file, possibility of exporting in plain text,
   portability.
2. Integrate the format into ETE, so annotated ETE trees (including graphical
   features) can be read, exported and exchanged with ease.
3. Develop basic converters from most common formats to date: i.e. Newick,
   Extended Newick and Nexus.

#### Possible approaches

* Use SQLite:
  See
  [this](https://github.com/etetoolkit/ete/blob/master/ete3/ncbi_taxonomy/ncbiquery.py) prototype
  API implementation currently used to store and query a very large tree
* Use a novel data format based indexing
  a
  [tabular tree format](https://github.com/jhcepas/tree_formats/blob/master/tree.ttf)
  

#### Difficulty
Medium

#### Languages and skills
* Good Python programming skills
* Experience on Object Oriented Programming in Python

#### Mentors
* Jaime Huerta-Cepas (EMBL, Germany)
* Francois Serra (CNAG-CRG, Spain)
* Renato Alves (EMBL, Germany)
* Łukasz Roguski (CNAG-CRG, Spain)

#### Contact 
ete-gsoc-mentors@googlegroups.com


### 2. Improve the usability of the command line tools and develop a Graphical User Interface (GUI) to execute jobs

#### Raionale 

[ETE-build](http://etetoolkit.org/documentation/ete-build/) is a command line
tool that provides a unified interface for the reproducible execution of complex
phylogenetic workflows. Those workflows are composed of several steps that
require calling multiple third-party programs as well as parsing and processing
results. At the moment, ETE-build can be used to easily execute those workflows
with a single command line. All the required tasks are then handled by an
internal scheduling system, so third party software is executed transparently.

#### Goals

1. Developing a graphical user interface that allows to run workflows and visualize results 
2. Adding windows support (currently only Linux and OSX are officially supported). 
3. Fixing and improving known issues in the scheduling and pipeline system
4. Adding new workflows and application bindings. 

#### Difficulty
Medium

#### Languages and skills
* Good Python programming skills
* Experience on Object Oriented Programming in Python
* Some tasks will require basic understanding of
  the
  [phylogenetic reconstruction](http://www.evolution-textbook.org/content/free/contents/ch27.html#ch27-2) process.

#### Mentors
* Jaime Huerta-Cepas (EMBL, Germany)
* Francois Serra (CNAG-CRG, Spain)
* Renato Alves (EMBL, Germany)

#### Contact 
ete-gsoc-mentors@googlegroups.com


### 3. Data visualization: developing a gallery of predefined tree layouts targeting publication ready figures

#### Rationale

Although the syntax of ETE’s tree rendering engine is highly flexible and allows
creating a variety
of [complex tree visualizations](http://etetoolkit.org/gallery/), this usually
involves substantial scripting work. Predefined layouts could be provided in the
form of ETE python scripts, that permit to style trees according to most common
usages. For instance, the following tree figures could be entirely renderable
using ETE, but not predefined scripts exist yet for that purpose:

[![alt text](http://etetoolkit.org/static/ete_gallery.png "ete gallery")](http://etetoolkit.org/gallery/)

#### Goals
* Develop a gallery of layouts in the form of Python scripts that cover most common visualizations in phylogenetics, including 
* Selection of good color schemes
* Deciding what graphical features to show or hide depending on context
* Improve ETE’s rendering system, so multiple layouts can be applied as semantic layers. For instance:

```TreeStyle.layout = [block_alignment_layout, color_duplication_nodes_layout, ….] ```

#### Difficulty
Easy (from a programming point of view, but good graphical designing skills necessary)

#### Languages and skills
* Good Python programming skills
* Experience on Object Oriented Programming in Python
* Good in data visualization

#### Mentors
* Jaime Huerta-Cepas (EMBL, Germany)
* Francois Serra (CNAG-CRG, Spain)
* Renato Alves (EMBL, Germany)

#### Contact 
ete-gsoc-mentors@googlegroups.com


### 4. Tree searching using regular-expression-like queries

#### Rationale

Although several methods allow comparing trees using ETE, no search capabilities
exist that permit to query tree topologies for specific patterns. The goal of
this project is to develop a new ETE module that allows querying large
collections of trees using custom criteria. Searches should be flexible and
allow for regular-expression-like queries, returning a list of all internal
nodes in the matching trees where the criteria is fulfilled.

Applications of the framework would enable any user to perform complex queries
on a variety of tree-like data in research, such as clustering results and
phylogenetic trees. This is **specially relevant** in the **Phylogenomics**
field (ETE focus), where thousands of phylogenetic trees are being generated and
scanned for specific evolutionary patterns. Based on previous ETE developments
and last-year GSoC work, a
prototype [tree-matcher program](https://github.com/etetoolkit/treematcher)
exists, which provides basic functionality and examples.

#### Goals

* Improve the [tree-matcher](https://github.com/etetoolkit/treematcher/blob/master/test_treematcher.py) module to permit searching for complex patterns (i.e. [allow for complex queries using wildcards](https://github.com/etetoolkit/treematcher/issues/22))  

* Improve and extend
  the
  [tree search command line tool](https://github.com/etetoolkit/treematcher/issues/17)
* Integrate tree-matcher as a new ETE module, including complete unitests and
  documentation.
* Optional: Develop a visualization framework based on ETE’s tree rendering
  engine to display tree matches and differences.

#### Difficulty
Medium

#### Languages and skill
* Good Python programming skills
* Experience on Object Oriented Programming in Python
* Familiarity with the [Newick Tree format ](https://en.wikipedia.org/wiki/Newick_format)and the concept of phylogenetic gene trees (i.e. see [this](http://biologos.org/blogs/dennis-venema-letters-to-the-duchess/evolution-basics-species-trees-gene-trees-and-incomplete-lineage-sorting/))
* Familiarity with tree related algorithms (i.e. tree traversing, tree
  comparison)
* Optional (for addressing visualization): familiarity of Qt4 drawing system
  (QGraphicsScenes)

#### **Mentors**
* Francois Serra (CNAG-CRG, Spain)
* Łukasz Roguski (CNAG-CRG, Spain)
* Jaime Huerta-Cepas (EMBL, Germany)
* Renato Alves (EMBL, Germany)

#### Contact 
ete-gsoc-mentors@googlegroups.com

