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
Python
Python troubleshooting

#### Code
https://github.com/common-workflow-language/gxargparse
https://github.com/common-workflow-language/common-workflow-language/issues/175#issuecomment-183332827

#### Mentors
[Roman Valls Guimera](https://github.com/brainstorm)
[Michael R. Crusoe](https://github.com/mr-c)
[Oliver Hofmann](https://github.com/ohofmann)

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
_Easy_ to _hard_, depending on the student's familiarity with the tools to be
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

_Project-dependent_

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
_medium_

#### Mentors
Max Ogden, Mathias Buus, Bruno Vieira, Yannik Wurm
