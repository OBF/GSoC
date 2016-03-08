---
layout: page
title: Project Ideas
permalink: /ideas/
---

# Google Summer of Code 2016 Project ideas

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


### Automated tool wrapper/converter for CWL

#### Rationale

The [Common Workflow Language](http://commonwl.org/) has so far defined a standard and a reference implementation to that standard, as opposed to the common practice of creating a system and then (not) trying to standardize it.

Defining [workflows](https://github.com/common-workflow-language/workflows) is a work in progress for CWL, but a more daunting task looms ahead of its adoption: wrapping tools.

Analogous to the packaging problem, we think that wrapping tools from already established systems such as Galaxy or Taverna is a task best done by machines. Unfortunately, there are no (automated) converters between those systems.

#### Approach

This project aims to solve part of that by taking [gxargparse](https://github.com/common-workflow-language/gxargparse), a proof of concept for the python tools command line ecosystem.

Internally, gxargparse, masquerading as argparse attempts to find and import the real argparse. 
It then stores a reference to the code module for the system argparse, and presents the user with all 
of the functions that stdlib argparse provides. Every function call is passed through the system argparse.

However, gxargparse captures the details of those calls and when a tool definition (Galaxy Tool XML in 
the case of the original code base) is requested, it builds up the tool definition according to community standards.

Another small proof of concept within the python ecosystem involves the docopt package and 
[rabixator](https://github.com/stefanristeski/rabixator). Furthermore, other similar instrumentation 
is being discussed to, for example, explore and optimize the parameter/flag space of i.e, bioinformatic
aligners with [Teaser](http://dx.doi.org/10.1186/s13059-015-0803-1).

Last but not least, if this approach could be generalized to tools written in other languages such as Java, 
C, Perl, among others, it would not only ease the migration of (bioinformatics) tools to newer workflow
systems, but for instance test the quality and robustness of several bioinformatics tools automatically.

#### Languages and skills
* Python
* Python troubleshooting

#### Code
* [https://github.com/common-workflow-language/gxargparse](https://github.com/common-workflow-language/gxargparse)
* [https://github.com/common-workflow-language/common-workflow-language/issues/175#issuecomment-183332827](https://github.com/common-workflow-language/common-workflow-language/issues/175#issuecomment-183332827)

#### Difficulty
<span class="medium">medium</span>

#### Mentors
[Roman Valls Guimera](https://github.com/brainstorm),
[Michael R. Crusoe](https://github.com/mr-c),
[Oliver Hofmann](https://github.com/ohofmann)

## Nextflow

### Nextflow integration with NCBI Sequence Read Archive (SRA) 

#### Rationale

Truly reproducible computational analysis relies on the having the exact same software, computational environment and data available. [Nextflow](http://www.nextflow.io/) along with [Docker](https://www.docker.com/) fulfills the software and environment requirements yet the data is kept distinct.

It now common practice that DNA and RNA sequencing data must be made available in the [NCBI Sequence Read Archive](http://www.ncbi.nlm.nih.gov/sra) (SRA). 
Integration of the SRA into Nextflow could allow users to reference, pull and analyse their or others read data in programmatic manner.
As an example, a user of pipeline could specify an SRA Study ID, for example the ID SRP003186 and have the mapping performed exactly as is specified in the study.

#### Approach 

The suggested approach consist in integrating the NCBI SRA toolkit into Nextflow in such a way that SRA entries can be accessed from a pipeline script extending the Nextflow built-in operators whenever necessary.

#### Languages and skills 

Student is required to have a good knowledge of the Java/C++ programming languages and some basic skills of NGS data analysis. 

#### Code

* [Nextflow source code repository](https://github.com/nextflow-io/nextflow)
* [NCBI SRA toolkit](https://github.com/ncbi/ncbi-vdb)
* [NCBI NGS language binding](https://github.com/ncbi/ngs)

#### Difficulty
<span class="medium">medium</span>

#### Mentors
Evan Floden, Maria Chatzou, Paolo Di Tommaso

### Nextflow support for Common Workflow Language  

#### Rationale

[Nextflow](http://www.nextflow.io/) is a lightweight framework for computational pipelines. It implements a domain specific language (DSL) 
that simplifies writing parallel and scalable pipelines in a portable manner across different execution platform.    

The [Common Workflow Language](http://commonwl.org/) (CWL) is a community effort to create a standard specification to define and describe 
data analysis workflows that can be implemented by tools and platforms. 

This proposal aims to implement in Nextflow a support for the CWL. This would allow any CWL defined pipeline to be executable 
with the Nextflow pipeline framework increasing the interoperability of the tool with other frameworks and platforms.   

####  Approach 

The approach suggested consists in the implementation of a conversion tool able to parse a CWL pipeline definition 
and translate it to an equivalent Nextflow DSL script. At a first stage this tool can be prototyped in any programming 
language as an independent program. Then it is required to be written in Java/Groovy and to be integrated in the Nextflow codebase.

#### Languages and skills
Student is required to have a good knowledge of the Java and/or Groovy programming languages and basic concepts of parallel programming and computational workflows.

####  Code 

* [Nextflow source code repository](https://github.com/nextflow-io/nextflow)
* [Common WL source code repository](https://github.com/common-workflow-language/common-workflow-language)

#### Mentors 

Paolo Di Tommaso, Pablo Prieto

### Nextflow user interface 

#### Rationale 

[Nextflow](http://www.nextflow.io/) is a lightweight framework for computational pipelines. It implements a domain specific language (DSL) that 
simplifies writing parallel and scalable pipelines in a portable manner across different execution platform. 

Nextflowhas been developed as a command line oriented tool because this allows developers a faster prototyping and development 
cycle and simplify the application deployment process. However end-users may not have the required skills to operate 
with the *-nix command line required to manage and launch a Nextflow based data analysis workflow. 

The proposed idea is to developed a lean web user interface that allows users to launch and monitor the execution a 
Nextflow based pipeline.  

#### Approach 

The suggested approach consist in splitting the project goal in two main work packages. The first requires to implement 
a REST based API in the Nextflow execution engine that allows a remote application to access the runtime information of a 
running pipeline (list of submitted tasks, task status, task execution details, etc.)  and to operate with it (pause, 
stop, resume execution).

The second package requires to implement a web based dashboard application that would allow a user to connect to a remote 
Nextflow instance and control its execution status by using the above API. Ideally the dashboard application should 
self-contained and able to run without requiring a prior installation of external dependencies.  

#### Languages and skills 

The student is required to have proven ability with Javascript, HTML5, Polymer. Experience with API design and a good 
knowledge of the Groovy/Java programming languages.

#### Code 

* [Nextflow source code repository](https://github.com/nextflow-io/nextflow)

#### Difficulty
<span class="medium">medium</span>

#### Mentors 

Emilio Palumbo, Paolo Di Tommaso


## BioPerl

* [Mailing lists](http://bioperl.org/wiki/Mailing_lists)
* IRC: `#bioperl` on [Freenode](http://freenode.net/)
* [Information for new developers](http://bioperl.org/wiki/Becoming_a_developer)
* Source code browser for [bioperl-live](https://github.com/bioperl/bioperl-live)
  (the main BioPerl code base) and [all BioPerl sub-projects](https://github.com/bioperl)
* [Priority list](http://bioperl.org/wiki/Project_priority_list) of things that need work,
  as another source for student-conceived project ideas

### NGS-friendly BioPerl code

#### Rationale
BioPerl is known to be slow re: any data sets, but particularly when dealing
with very large data (e.g. anything related to NGS analysis. Can we make it
better? Where should we focus our efforts?

#### Approach
Under the supervision of their mentor(s), the GSoC student will:

* Benchmark bottlenecks that lead to loss in performance for NGS analyses
* Refactor old classes or develop new optimized code for NGS analysis

#### Languages and skills
The main part of the project is going to be in Perl, some C knowledge might be
helpful if C library bindings can be used.

Skills required:

* excellent Perl programming skills
* knowledge of modern Perl practices
* familiarity with Next Generation Sequencing (NGS) datasets is a plus

#### Difficulty
<span class="easy">easy</span> to <span class="hard">hard</span>, depending on the student's familiarity with the tools to be
used.

#### Mentors
Chris Fields, Mark Jensen


### BioPerl 2.0 / BioPerl6

#### Rationale
Design or reimplement BioPerl classes without API constraint, using Modern Perl
tools or Perl 6.

#### Approach 1
Perl6 was released late last year. This gives us an enormous opportunity to
redesign fundamental aspects of BioPerl without the necessity for development
hindered by a requirement for backwards compatibility.

See also: [BioPerl6 proof of concept](http://github.com/cjfields/bioperl6)

#### Approach 2

Most BioPerl code is over 6 years old and doesn't take advantage of Modern Perl
tools, such as new methods in later versions of perl, Template:CPAN/MooseX,
Template:CPAN, and more. Set up the basic core classes that allow mingling of
Modern Perl with older BioPerl classes; propose and benchmark variations of
specific core classes utilizing Modern Perl tools.

See also [Biome (Moose-based BioPerl) proof of
concept](http://github.com/cjfields/bioperl6)

#### Difficulty

_Project-dependent_, <span class="easy">easy</span> to <span
class="hard">hard</span>

#### Mentors
Chris Fields, Mark Jensen


## Bionode

### Bionode workflow engine for streamed data analysis

#### Rationale

Researchers should be able to:

* Perform analyses while data are generated (i.e., with “data streams”);
* Easily and rapidly update results if input data or analysis
  approaches/parameters change (with minimal recomputation);
* Effortlessly change and scale underlying computing platforms while
  pipeline is running;
* Easily visualise results.

This is largely impossible because current approaches were developed
when datasets were simpler and smaller. The student will take
advantage of recent improvements in generic analysis tools (Node.js
Streams & asynchronous concurrency) to attain the above objectives.

#### Approach
The student will create a workflow engine for streamed data analysis
with concurrent pipelining. The main mentors will be Max Ogden and
Mathias Buus, top Node.js contributors and founders of Dat-data.com,
for their experience with streaming interfaces. Bruno Vieira
(founder of Bionode.io) and Yannick Wurm (lecturer in Bioinformatics
at QMUL) will co-supervise.

Some work on the data structures and programming interfaces for
commonly used data sources (e.g., NCBI, Uniprot, Ensembl/Biomart)
and data types (e.g., VCF, BAM, FASTQ) will be required.

The underlying computational architecture architecture should be
abstracted. This means that analysis code will run identically using
different traditional high performance computing system (e.g.,
Torque, SGE) and modern systems (e.g., Hadoop MapReduce).

#### Languages and skill
JavaScript skills are required. Node.js and some biology knowledge
is a plus. Difficulty is medium.

#### Code
Some components and proof of concepts required for this project are
available at [http://github.com/bionode](http://github.com/bionode)

#### Difficulty
<span class="medium">medium</span>

#### Mentors
Max Ogden, Mathias Buus, Bruno Vieira, Yannick Wurm

## antiSMASH

[antiSMASH](http://antismash.secondarymetabolites.org) is a tool to mine the
genomes of micro-organisms for biologically interesting gene clusters, so-called
secondary metabolites, to help find new antibiotics. It is a python-based  open
source tool that is developed at the Danish Technical University and Wageningen
University.

Project ideas around antiSMASH range from very close to applied biology to more
general software engineering projects.

### Improve the prediction for RiPP clusters

#### Rationale
Ribosomally synthesised and post-translationally modified peptides (RiPPs) are a
class of secondary metabolites that are produced from a precursor gene encoded
on the genome of a microorganism. It is translated to a peptide by the ribosome,
and then further modified to give the active final product.

#### Approach

In this project, prediction modules for a number of RiPP clusters will be
developed. Working together with the mentors, who can provide advice both from
the technical as well as scientific side of the project, the student will create
antiSMMASH plug-ins.

Each plug-in handles three distinct steps:

1. Detect the RiPP precursor gene
2. Identify where the leader/tail peptitdes are cleaved from the core peptide
3. Predict any further modifications to the core peptide.

Additionally, plug-ins also handle creating html output to optimally present
their predictions to researchers.

#### Languages and skill
antiSMASH is written in Python 2.7. Some basic genetics/molecular biology
background will make this project easier, but is not a requirement.

#### Code
* [antiSMASH on Bitbucket](https://bitbucket.org/antismash/antismash)
* Code will work similar to the [lantipeptide
  module](https://bitbucket.org/antismash/antismash/src/088f2a9cf7742b7ff79333dfecab5e4f86d3319e/antismash/specific_modules/lantipeptides/?at=master)

#### Difficulty
* <span class="easy">easy</span> if the biological background is known already
* <span class="medium">medium</span> otherwise

#### Mentors
[Kai Blin](https://github.com/kblin), Tilmann Weber


### SeqRecord access abstraction layer

#### Rationale
Internally, antiSMASH uses BioPython SeqRecord objects to handle the data. A lot
of the annotations are in custom feature entries or in free-text qualifiers of
"gene"3 or "CDS" features. Code for handling this access is duplicated in parts
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

## GeneNetwork Genome Browser (biodalliance)

[GeneNetwork.org](http://gn2.genenetwork.org/) (GN) is a Web2.0
environment for genetic analysis in mouse, rat and human (QTL mapping
and GWAS). GN ised daily by scientists with over a thousand
publications citing it.

[Biodiallance.org](http://www.biodalliance.org/) is a state-of-the-art
Javascript genome browser. It is a fast, interactive, genome
visualization tool that's easy to embed in web pages and
applications. It supports integration of data from a wide variety of
sources, and can load data directly from popular genomics file formats
including bigWig, BAM, and VCF. Biodiallance has been adopted by some
major bioinformatics websites.

#### Rationale

To improve user experience and improve biomedical discovery potential
we want to add advanced visualisation and embed the state-of-the-art
[biodiallance genome browser](http://www.biodalliance.org/) into GN
and add several new *tracks* for visualizing mapped QTL, underlying
genotypes and SNP density.

![Biodalliance](https://sagebionetworks.jira.com/secure/attachment/24449/biodalliance%20widget%20output.png)

#### Approach

BioDiallance has good abstractions for tracks and fetching data. We
will look into fetching data on-the-fly from GN backends through a
REST interface. Also we will add interaction that when a user [clicks
on a QTL](http://kbroman.org/qtlcharts/example/iplotScanone.html), for example, the browser can display additional information
and even initiate some back-end processing.

We will use continuous
[open channels](http://www.phoenixframework.org/) between the browser
and the backend.

#### Languages and skill

Biodiallance is written in Javascript. GeneNetwork is mostly python
and Javascript.  The GN REST interface is written in Elixir.

#### Code

* [Genenetwork.org](https://github.com/genenetwork)
* [Biodalliance](https://github.com/dasmoth/dalliance)

#### Difficulty
* <span class="medium">medium</span> mostly Javascript, but python and elixir may come in handy

#### Mentors
[Pjotr Prins](https://github.com/pjotrp), [Karl Broman](https://github.com/kbroman)

#### Contact

* IRC: `#genenetwork` on [Freenode](http://freenode.net/)
* [Mailing list GeneNetwork](http://listserv.uthsc.edu/mailman/listinfo/genenetwork-dev)
* [Mailing list Biodalliance](https://groups.google.com/forum/#!forum/biodalliance-dev)
* Direct: pjotr.public345 at thebird.nl

## ETE Toolkit

[ETE](http://etetoolkit.org) is a Python framework for the analysis and
visualization of trees, commonly used for the analysis of
[phylogenetic trees](https://en.wikipedia.org/wiki/Phylogenetic_tree) and in other research areas. 


* [Mailing list](https://groups.google.com/forum/#!forum/etetoolkit)
* [Source code](https://github.com/etetoolkit/ete)

### Tree searching using regular-expression-like queries

#### Rationale

Although several methods allow comparing trees using ETE, no search capabilities
exist that permit to query tree topologies for specific patterns. The goal of
this project is to develop a new ETE module that allows querying large
collections of trees using custom criteria. Searches should be flexible and
allow for regular-expression-like queries, returning a list of all internal
nodes in the matching trees where the criteria is fulfilled.

Applications of the framework would enable any user to perform
complex queries on a variate of tree-like data in research, such as
clustering results and phylogenetic trees. This is **specially relevant**
in the **Phylogenomics**  field (ETE focus), where thousands of
phylogenetic trees are being generated and scanned for specific
evolutionary patterns.

Optional goal: Matches and differences between trees and queries could further be
visualized using ETE's rendering engine, which will involve the creation of
custom visualization layouts.

#### Approach
Under the supervision of their mentors, the GSoC student will:

* Implement a system for searching within ETE Tree structures. 
* Develop a vocabulary of queries that permit regular-expression-like queries. 
* Integrate the framework as a new ETE module, including unitests and documentation. 
* Optional: Develop a visualization framework based on ETE's tree rendering engine to
  display tree matches and differences.
 
#### Languages and skills

All code should be written in Python, with compatibility for Py2 and Py3.

Skills required:

* Good Python programming skills
* Experience on Object Oriented Programming in Python 
* Familiarity with tree related algorithms (i.e. tree traversing, tree comparison)
* Optional (for addressing visualization): familiarity of Qt4 drawing system (QGraphicsScenes)

#### Difficulty 

<span class="medium">medium</span>

#### Mentors
[Jaime Huerta-Cepas](http://github.com/jhcepas), [Renato Alves](http://github.com/unode), [Francois Serra](http://github.com/fransua)

### Extend tree visualization capabilities

#### Rationale

Tree visualization with ETE allows for advanced customizing of rectangular and
circular tree images, being used to display 
[different types](http://etetoolkit.org/gallery/) of biological results. However, the
following features are currently missing and commonly requested by users:

* Plotting horizontal links between branches (useful to, for instance, display
  [Horizontal Gene Transfers](https://en.wikipedia.org/wiki/Horizontal_gene_transfer))
* Drawing [time-calibrated trees](https://github.com/etetoolkit/ete/issues/112)
* Improving SVG rendering (better web integration of tree images)

This project aims at covering as many of those features as possible, but the
student could choose to focus on only one.

#### Approach
Under the supervision of their mentors, the GSoC student will work on:

* Implementing a new rendering layer for visualizing
  [Horizontal Gene Transfer (HGT)](https://en.wikipedia.org/wiki/Horizontal_gene_transfer)
  events.  The implementation should be done on top of the current rendering
  engine, by adding the capability of translating horizontal node links created
  programmatically (i.e. `node1.add_link(node2)`) into visual links in the final
  tree image. A prototype is discussed [here](https://github.com/etetoolkit/ete/issues/161). 
  
  
* Improving SVG rendering capabilities permitting better web
  integration. Although the implementation of a fully-capable web viewer is out
  of the scope, the creation of annotated SVG images (i.e. node IDs being added
  to SVG elements) could be used to produce basic interactive SVG tree
  images. Currently, an experimental static version of ETE based SVG images exist
  [here](http://etetoolkit.org/treeview), and could be used as a starting point
  for development.
    
* Adding new graphical elements to the collection of
  [ETE Faces](http://etetoolkit.org/docs/latest/reference/reference_treeview.html#faces). Most
  notably, the addition of branch-length-rulers which can be correctly aligned to tree branches, and 
  the implementation of specific layouts. 

#### Languages and skills

All code will be in Python, with compatibility for Py2 and Py3 and using Qt4 as
the image rendering library.

Skills required:

* Excellent Python programming skills
* Experience on Object Oriented Programming in Python 
* Familiarity with tree related algorithms (i.e. tree traversing)
* Familiarity with Qt4 drawing system (QGraphicsScene)
* basic knowledge on web development (HTML/javascript)

#### Difficulty 

<span class="medium">medium</span> to <span class="hard">hard</span>, depending on
student's capabilities and the tasks selected.

#### Mentors
[Jaime Huerta-Cepas](http://github.com/jhcepas), [Renato Alves](http://github.com/unode), [Francois Serra](http://github.com/fransua)



